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
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a><span data-ttu-id="4b851-103">適用於 C 的 Azure IoT 裝置 SDK - 深入了解序列化程式</span><span class="sxs-lookup"><span data-stu-id="4b851-103">Azure IoT device SDK for C – more about serializer</span></span>
<span data-ttu-id="4b851-104">hello[先文章](iot-hub-device-sdk-c-intro.md)中這個數列導入 hello **C 的 Azure IoT 裝置 SDK**。 hello 下一篇文章提供更詳細的描述的 hello [ **IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="4b851-104">hello [first article](iot-hub-device-sdk-c-intro.md) in this series introduced hello **Azure IoT device SDK for C**. hello next article provided a more detailed description of hello [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="4b851-105">這篇文章提供更詳細的描述的其餘元件 hello 完成 hello SDK 的涵蓋範圍： hello**序列化程式**程式庫。</span><span class="sxs-lookup"><span data-stu-id="4b851-105">This article completes coverage of hello SDK by providing a more detailed description of hello remaining component: hello **serializer** library.</span></span>

<span data-ttu-id="4b851-106">hello 簡介文章所述方式 toouse hello**序列化程式**文件庫 toosend 事件 tooand 從 IoT 中心接收訊息。</span><span class="sxs-lookup"><span data-stu-id="4b851-106">hello introductory article described how toouse hello **serializer** library toosend events tooand receive messages from IoT Hub.</span></span> <span data-ttu-id="4b851-107">在本文中延伸，討論藉由提供方式的更完整的說明 toomodel 資料以 hello**序列化程式**巨集語言。</span><span class="sxs-lookup"><span data-stu-id="4b851-107">In this article, we extend that discussion by providing a more complete explanation of how toomodel your data with hello **serializer** macro language.</span></span> <span data-ttu-id="4b851-108">hello 文章也包含更多詳細 hello 程式庫將訊息的序列化，並在某些情況下如何控制 hello 序列化行為。</span><span class="sxs-lookup"><span data-stu-id="4b851-108">hello article also includes more detail about how hello library serializes messages (and in some cases how you can control hello serialization behavior).</span></span> <span data-ttu-id="4b851-109">我們也將說明您可以修改判斷 hello 大小，您所建立的 hello 模型的某些參數。</span><span class="sxs-lookup"><span data-stu-id="4b851-109">We'll also describe some parameters you can modify that determine hello size of hello models you create.</span></span>

<span data-ttu-id="4b851-110">最後，hello 發行項會重新審視某些訊息等屬性處理的上一個文件中涵蓋的主題。</span><span class="sxs-lookup"><span data-stu-id="4b851-110">Finally, hello article revisits some topics covered in previous articles such as message and property handling.</span></span> <span data-ttu-id="4b851-111">因為我們會了解，這些功能的運作在 hello 相同方式使用 hello**序列化程式**文件庫以 hello 一樣**IoTHubClient**程式庫。</span><span class="sxs-lookup"><span data-stu-id="4b851-111">As we'll find out, those features work in hello same way using hello **serializer** library as they do with hello **IoTHubClient** library.</span></span>

<span data-ttu-id="4b851-112">本文中所述的所有項目根據 hello**序列化程式**SDK 範例。</span><span class="sxs-lookup"><span data-stu-id="4b851-112">Everything described in this article is based on hello **serializer** SDK samples.</span></span> <span data-ttu-id="4b851-113">如果您想沿著 toofollow，請參閱 hello **simplesample\_amqp**和**simplesample\_http** C.hello Azure IoT 裝置 SDK 中所包含的應用程式</span><span class="sxs-lookup"><span data-stu-id="4b851-113">If you want toofollow along, see hello **simplesample\_amqp** and **simplesample\_http** applications included in hello Azure IoT device SDK for C.</span></span>

<span data-ttu-id="4b851-114">您可以找到 hello [ **C 的 Azure IoT 裝置 SDK** ](https://github.com/Azure/azure-iot-sdk-c) GitHub 儲存機制和檢視詳細資料的 hello API 在 hello [C 應用程式開發介面參考](https://azure.github.io/azure-iot-sdk-c/index.html)。</span><span class="sxs-lookup"><span data-stu-id="4b851-114">You can find hello [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of hello API in hello [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="hello-modeling-language"></a><span data-ttu-id="4b851-115">hello 模組化語言</span><span class="sxs-lookup"><span data-stu-id="4b851-115">hello modeling language</span></span>
<span data-ttu-id="4b851-116">hello[簡介文章](iot-hub-device-sdk-c-intro.md)中這個數列導入 hello **C 的 Azure IoT 裝置 SDK**模組化語言 hello 中所提供的 hello 範例透過**simplesample\_amqp**應用程式：</span><span class="sxs-lookup"><span data-stu-id="4b851-116">hello [introductory article](iot-hub-device-sdk-c-intro.md) in this series introduced hello **Azure IoT device SDK for C** modeling language through hello example provided in hello **simplesample\_amqp** application:</span></span>

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

<span data-ttu-id="4b851-117">如您所見，hello 模組化語言是以 C 巨集為基礎。</span><span class="sxs-lookup"><span data-stu-id="4b851-117">As you can see, hello modeling language is based on C macros.</span></span> <span data-ttu-id="4b851-118">您的定義開頭一律會是 **BEGIN\_NAMESPACE**，而結尾則一律是 **END\_NAMESPACE**。</span><span class="sxs-lookup"><span data-stu-id="4b851-118">You always begin your definition with **BEGIN\_NAMESPACE** and always end with **END\_NAMESPACE**.</span></span> <span data-ttu-id="4b851-119">它是一般 tooname hello 命名空間為您的公司或如同此範例中，您正在使用的 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="4b851-119">It's common tooname hello namespace for your company or, as in this example, hello project that you're working on.</span></span>

<span data-ttu-id="4b851-120">Hello 命名空間內的元素是一種模型定義。</span><span class="sxs-lookup"><span data-stu-id="4b851-120">What goes inside hello namespace are model definitions.</span></span> <span data-ttu-id="4b851-121">在此案例中，有一個單一的風速計模型。</span><span class="sxs-lookup"><span data-stu-id="4b851-121">In this case, there is a single model for an anemometer.</span></span> <span data-ttu-id="4b851-122">同樣地，hello 模型可以命名為任何項目，但通常此節點稱為 hello 裝置或類型的資料要 tooexchange 與 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="4b851-122">Once again, hello model can be named anything, but typically this is named for hello device or type of data you want tooexchange with IoT Hub.</span></span>  

<span data-ttu-id="4b851-123">模型包含定義的 hello 事件中，您可以輸入 tooIoT 中樞 (hello*資料*) 以及您可以從 IoT 中樞接收 hello 訊息 (hello*動作*)。</span><span class="sxs-lookup"><span data-stu-id="4b851-123">Models contain a definition of hello events you can ingress tooIoT Hub (hello *data*) as well as hello messages you can receive from IoT Hub (hello *actions*).</span></span> <span data-ttu-id="4b851-124">您可以看到 hello 範例中，事件具有類型和欄位名稱。動作都有一個名稱和選擇性的參數 （各有型別）。</span><span class="sxs-lookup"><span data-stu-id="4b851-124">As you can see from hello example, events have a type and a name; actions have a name and optional parameters (each with a type).</span></span>

<span data-ttu-id="4b851-125">並不會在此範例中示範是 hello SDK 所支援的其他資料型別。</span><span class="sxs-lookup"><span data-stu-id="4b851-125">What’s not demonstrated in this sample are additional data types that are supported by hello SDK.</span></span> <span data-ttu-id="4b851-126">我們將在稍後討論。</span><span class="sxs-lookup"><span data-stu-id="4b851-126">We'll cover that next.</span></span>

> [!NOTE]
> <span data-ttu-id="4b851-127">IoT 中樞是指 toohello 資料的裝置傳送為 tooit*事件*，而 hello 模組化語言參考做為 tooit*資料*(使用定義**WITH_DATA**)。</span><span class="sxs-lookup"><span data-stu-id="4b851-127">IoT Hub refers toohello data a device sends tooit as *events*, while hello modeling language refers tooit as *data* (defined using **WITH_DATA**).</span></span> <span data-ttu-id="4b851-128">同樣地，IoT 中樞是指 toohello 資料傳送為 toodevices*訊息*，而 hello 模組化語言參考做為 tooit*動作*(使用定義**WITH_ACTION**)。</span><span class="sxs-lookup"><span data-stu-id="4b851-128">Likewise, IoT Hub refers toohello data you send toodevices as *messages*, while hello modeling language refers tooit as *actions* (defined using **WITH_ACTION**).</span></span> <span data-ttu-id="4b851-129">請注意，在本文中可能會交替使用這些詞彙。</span><span class="sxs-lookup"><span data-stu-id="4b851-129">Be aware that these terms may be used interchangeably in this article.</span></span>
> 
> 

### <a name="supported-data-types"></a><span data-ttu-id="4b851-130">支援的資料類型</span><span class="sxs-lookup"><span data-stu-id="4b851-130">Supported data types</span></span>
<span data-ttu-id="4b851-131">建立 hello 的模型中支援下列資料類型的 hello**序列化程式**程式庫：</span><span class="sxs-lookup"><span data-stu-id="4b851-131">hello following data types are supported in models created with hello **serializer** library:</span></span>

| <span data-ttu-id="4b851-132">類型</span><span class="sxs-lookup"><span data-stu-id="4b851-132">Type</span></span> | <span data-ttu-id="4b851-133">說明</span><span class="sxs-lookup"><span data-stu-id="4b851-133">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4b851-134">double</span><span class="sxs-lookup"><span data-stu-id="4b851-134">double</span></span> |<span data-ttu-id="4b851-135">雙精確度浮點數</span><span class="sxs-lookup"><span data-stu-id="4b851-135">double precision floating point number</span></span> |
| <span data-ttu-id="4b851-136">int</span><span class="sxs-lookup"><span data-stu-id="4b851-136">int</span></span> |<span data-ttu-id="4b851-137">32 位元整數</span><span class="sxs-lookup"><span data-stu-id="4b851-137">32 bit integer</span></span> |
| <span data-ttu-id="4b851-138">float</span><span class="sxs-lookup"><span data-stu-id="4b851-138">float</span></span> |<span data-ttu-id="4b851-139">單精確度浮點數</span><span class="sxs-lookup"><span data-stu-id="4b851-139">single precision floating point number</span></span> |
| <span data-ttu-id="4b851-140">long</span><span class="sxs-lookup"><span data-stu-id="4b851-140">long</span></span> |<span data-ttu-id="4b851-141">長整數</span><span class="sxs-lookup"><span data-stu-id="4b851-141">long integer</span></span> |
| <span data-ttu-id="4b851-142">int8\_t</span><span class="sxs-lookup"><span data-stu-id="4b851-142">int8\_t</span></span> |<span data-ttu-id="4b851-143">8 位元整數</span><span class="sxs-lookup"><span data-stu-id="4b851-143">8 bit integer</span></span> |
| <span data-ttu-id="4b851-144">int16\_t</span><span class="sxs-lookup"><span data-stu-id="4b851-144">int16\_t</span></span> |<span data-ttu-id="4b851-145">16 位元整數</span><span class="sxs-lookup"><span data-stu-id="4b851-145">16 bit integer</span></span> |
| <span data-ttu-id="4b851-146">int32\_t</span><span class="sxs-lookup"><span data-stu-id="4b851-146">int32\_t</span></span> |<span data-ttu-id="4b851-147">32 位元整數</span><span class="sxs-lookup"><span data-stu-id="4b851-147">32 bit integer</span></span> |
| <span data-ttu-id="4b851-148">int64\_t</span><span class="sxs-lookup"><span data-stu-id="4b851-148">int64\_t</span></span> |<span data-ttu-id="4b851-149">64 位元整數</span><span class="sxs-lookup"><span data-stu-id="4b851-149">64 bit integer</span></span> |
| <span data-ttu-id="4b851-150">布林</span><span class="sxs-lookup"><span data-stu-id="4b851-150">bool</span></span> |<span data-ttu-id="4b851-151">布林值</span><span class="sxs-lookup"><span data-stu-id="4b851-151">boolean</span></span> |
| <span data-ttu-id="4b851-152">ascii\_char\_ptr</span><span class="sxs-lookup"><span data-stu-id="4b851-152">ascii\_char\_ptr</span></span> |<span data-ttu-id="4b851-153">ASCII 字串</span><span class="sxs-lookup"><span data-stu-id="4b851-153">ASCII string</span></span> |
| <span data-ttu-id="4b851-154">EDM\_DATE\_TIME\_OFFSET</span><span class="sxs-lookup"><span data-stu-id="4b851-154">EDM\_DATE\_TIME\_OFFSET</span></span> |<span data-ttu-id="4b851-155">日期時間位移</span><span class="sxs-lookup"><span data-stu-id="4b851-155">date time offset</span></span> |
| <span data-ttu-id="4b851-156">EDM\_GUID</span><span class="sxs-lookup"><span data-stu-id="4b851-156">EDM\_GUID</span></span> |<span data-ttu-id="4b851-157">GUID</span><span class="sxs-lookup"><span data-stu-id="4b851-157">GUID</span></span> |
| <span data-ttu-id="4b851-158">EDM\_BINARY</span><span class="sxs-lookup"><span data-stu-id="4b851-158">EDM\_BINARY</span></span> |<span data-ttu-id="4b851-159">binary</span><span class="sxs-lookup"><span data-stu-id="4b851-159">binary</span></span> |
| <span data-ttu-id="4b851-160">DECLARE\_STRUCT</span><span class="sxs-lookup"><span data-stu-id="4b851-160">DECLARE\_STRUCT</span></span> |<span data-ttu-id="4b851-161">複雜資料類型</span><span class="sxs-lookup"><span data-stu-id="4b851-161">complex data type</span></span> |

<span data-ttu-id="4b851-162">讓我們開始 hello 最後一個資料類型。</span><span class="sxs-lookup"><span data-stu-id="4b851-162">Let’s start with hello last data type.</span></span> <span data-ttu-id="4b851-163">hello **DECLARE\_結構**可讓您 toodefine 複雜資料型別，也就是群組的 hello 其他基本型別。</span><span class="sxs-lookup"><span data-stu-id="4b851-163">hello **DECLARE\_STRUCT** allows you toodefine complex data types, which are groupings of hello other primitive types.</span></span> <span data-ttu-id="4b851-164">這些群組可讓我們 toodefine 的模型，看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="4b851-164">These groupings allow us toodefine a model that looks like this:</span></span>

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

<span data-ttu-id="4b851-165">我們的模型包含 **TestType**類型的單一資料事件。</span><span class="sxs-lookup"><span data-stu-id="4b851-165">Our model contains a single data event of type **TestType**.</span></span> <span data-ttu-id="4b851-166">**TestType**是包含數個成員，統稱為示範 hello hello 所支援的基本型別之複雜型別的**序列化程式**模組化語言。</span><span class="sxs-lookup"><span data-stu-id="4b851-166">**TestType** is a complex type that includes several members, which collectively demonstrate hello primitive types supported by hello **serializer** modeling language.</span></span>

<span data-ttu-id="4b851-167">使用像這樣的模型，我們可以撰寫程式碼 toosend 資料 tooIoT 集線器出現，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4b851-167">With a model like this, we can write code toosend data tooIoT Hub that appears as follows:</span></span>

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

<span data-ttu-id="4b851-168">基本上，我們正在指派值的 hello tooevery 成員**測試**結構，然後再呼叫**SendAsync** toosend hello**測試**資料事件 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="4b851-168">Basically, we’re assigning a value tooevery member of hello **Test** structure and then calling **SendAsync** toosend hello **Test** data event toohello cloud.</span></span> <span data-ttu-id="4b851-169">**SendAsync**會傳送單一資料事件 tooIoT 中樞的 helper 函式：</span><span class="sxs-lookup"><span data-stu-id="4b851-169">**SendAsync** is a helper function that sends a single data event tooIoT Hub:</span></span>

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

<span data-ttu-id="4b851-170">此函式序列化 hello 指定之資料的事件，並將它傳送 tooIoT 集線器使用**IoTHubClient\_SendEventAsync**。</span><span class="sxs-lookup"><span data-stu-id="4b851-170">This function serializes hello given data event and sends it tooIoT Hub using **IoTHubClient\_SendEventAsync**.</span></span> <span data-ttu-id="4b851-171">這是相同的程式碼中前一個發行項所討論的 hello (**SendAsync**封裝 hello 邏輯到方便的函式)。</span><span class="sxs-lookup"><span data-stu-id="4b851-171">This is hello same code discussed in previous articles (**SendAsync** encapsulates hello logic into a convenient function).</span></span>

<span data-ttu-id="4b851-172">一個 hello 先前的程式碼中使用其他 helper 函式是**GetDateTimeOffset**。</span><span class="sxs-lookup"><span data-stu-id="4b851-172">One other helper function used in hello previous code is **GetDateTimeOffset**.</span></span> <span data-ttu-id="4b851-173">此函式轉換成值類型的特定時間的 hello **EDM\_日期\_時間\_位移**:</span><span class="sxs-lookup"><span data-stu-id="4b851-173">This function transforms hello given time into a value of type **EDM\_DATE\_TIME\_OFFSET**:</span></span>

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

<span data-ttu-id="4b851-174">如果您執行此程式碼，hello 下訊息會傳送 tooIoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="4b851-174">If you run this code, hello following message is sent tooIoT Hub:</span></span>

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

<span data-ttu-id="4b851-175">請注意，hello 序列化為 JSON，這是產生的 hello hello 格式**序列化程式**程式庫。</span><span class="sxs-lookup"><span data-stu-id="4b851-175">Note that hello serialization is JSON, which is hello format generated by hello **serializer** library.</span></span> <span data-ttu-id="4b851-176">也請注意，每個成員的 hello 序列化 JSON 物件會比對的 hello hello 成員**TestType**我們在我們的模型定義。</span><span class="sxs-lookup"><span data-stu-id="4b851-176">Also note that each member of hello serialized JSON object matches hello members of hello **TestType** that we defined in our model.</span></span> <span data-ttu-id="4b851-177">hello 值也完全符合 hello 程式碼中使用。</span><span class="sxs-lookup"><span data-stu-id="4b851-177">hello values also exactly match those used in hello code.</span></span> <span data-ttu-id="4b851-178">不過，請注意，會以 base64 編碼 hello 二進位資料:"AQID 」 是 base64 編碼的 hello {0x01、 0x02、 0x03}。</span><span class="sxs-lookup"><span data-stu-id="4b851-178">However, note that hello binary data is base64-encoded: "AQID" is hello base64 encoding of {0x01, 0x02, 0x03}.</span></span>

<span data-ttu-id="4b851-179">這個範例會示範使用 hello 的 hello 優點**序列化程式**程式庫-它可讓我們 toosend JSON toohello 雲端，而不需要 tooexplicitly 處理我們的應用程式中的序列化。</span><span class="sxs-lookup"><span data-stu-id="4b851-179">This example demonstrates hello advantage of using hello **serializer** library -- it enables us toosend JSON toohello cloud, without having tooexplicitly deal with serialization in our application.</span></span> <span data-ttu-id="4b851-180">這些了解 tooworry 在我們的模型，然後再呼叫這些事件 toohello 雲端簡單的應用程式開發介面 toosend 設定 hello hello 值資料事件。</span><span class="sxs-lookup"><span data-stu-id="4b851-180">All we have tooworry about is setting hello values of hello data events in our model and then calling simple APIs toosend those events toohello cloud.</span></span>

<span data-ttu-id="4b851-181">利用此資訊，我們可以定義包含支援的資料類型，包括複雜型別 （我們甚至無法包含其他複雜類型內的複雜類型） 的 hello 範圍的模型。</span><span class="sxs-lookup"><span data-stu-id="4b851-181">With this information, we can define models that include hello range of supported data types, including complex types (we could even include complex types within other complex types).</span></span> <span data-ttu-id="4b851-182">不過，他序列化 JSON 產生的 hello 上述範例會顯示很重要的一點。</span><span class="sxs-lookup"><span data-stu-id="4b851-182">However, he serialized JSON generated by hello example above brings up an important point.</span></span> <span data-ttu-id="4b851-183">*如何*我們傳送給資料以 hello**序列化程式**程式庫可讓您判斷完全 hello JSON 形成方式。</span><span class="sxs-lookup"><span data-stu-id="4b851-183">*How* we send data with hello **serializer** library determines exactly how hello JSON is formed.</span></span> <span data-ttu-id="4b851-184">此特點就是我們接下來要討論的內容。</span><span class="sxs-lookup"><span data-stu-id="4b851-184">That particular point is what we'll cover next.</span></span>

## <a name="more-about-serialization"></a><span data-ttu-id="4b851-185">深入了解序列化</span><span class="sxs-lookup"><span data-stu-id="4b851-185">More about serialization</span></span>
<span data-ttu-id="4b851-186">hello 上一節會反白顯示 hello 所產生的輸出 hello 範例**序列化程式**程式庫。</span><span class="sxs-lookup"><span data-stu-id="4b851-186">hello previous section highlights an example of hello output generated by hello **serializer** library.</span></span> <span data-ttu-id="4b851-187">在本節中，我們將說明 hello 程式庫將資料序列化，以及如何控制使用 hello 序列化應用程式開發介面的行為。</span><span class="sxs-lookup"><span data-stu-id="4b851-187">In this section, we'll explain how hello library serializes data and how you can control that behavior using hello serialization APIs.</span></span>

<span data-ttu-id="4b851-188">在進行序列化時的順序 tooadvance hello 討論，我們將會使用新的模型根據 thermostat。</span><span class="sxs-lookup"><span data-stu-id="4b851-188">In order tooadvance hello discussion on serialization, we'll work with a new model based on a thermostat.</span></span> <span data-ttu-id="4b851-189">首先，我們提供一些背景 hello 案例中，我們正嘗試 tooaddress。</span><span class="sxs-lookup"><span data-stu-id="4b851-189">First, let's provide some background on hello scenario we're trying tooaddress.</span></span>

<span data-ttu-id="4b851-190">我們想要測量的溫度和溼度 thermostat toomodel。</span><span class="sxs-lookup"><span data-stu-id="4b851-190">We want toomodel a thermostat that measures temperature and humidity.</span></span> <span data-ttu-id="4b851-191">每個資料片段即將 toobe 以不同的方式傳送 tooIoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="4b851-191">Each piece of data is going toobe sent tooIoT Hub differently.</span></span> <span data-ttu-id="4b851-192">根據預設，hello thermostat ingresses 溫度事件一次每 2 分鐘。溼度事件是一次每隔 15 分鐘 ingressed。</span><span class="sxs-lookup"><span data-stu-id="4b851-192">By default, hello thermostat ingresses a temperature event once every 2 minutes; a humidity event is ingressed once every 15 minutes.</span></span> <span data-ttu-id="4b851-193">Ingressed 任一事件時，它必須包含該 hello 對應溫度顯示 hello 時間的時間戳記或測量溼度。</span><span class="sxs-lookup"><span data-stu-id="4b851-193">When either event is ingressed, it must include a timestamp that shows hello time that hello corresponding temperature or humidity was measured.</span></span>

<span data-ttu-id="4b851-194">提供此案例中，我們將示範兩個不同的方式 toomodel hello 資料，及我們將說明該模型已在 hello 序列化輸出的 hello 效果。</span><span class="sxs-lookup"><span data-stu-id="4b851-194">Given this scenario, we'll demonstrate two different ways toomodel hello data, and we'll explain hello effect that modeling has on hello serialized output.</span></span>

### <a name="model-1"></a><span data-ttu-id="4b851-195">模型 1</span><span class="sxs-lookup"><span data-stu-id="4b851-195">Model 1</span></span>
<span data-ttu-id="4b851-196">以下是模型的 hello 第一個版本支援 hello 前一個案例：</span><span class="sxs-lookup"><span data-stu-id="4b851-196">Here's hello first version of a model that supports hello previous scenario:</span></span>

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

<span data-ttu-id="4b851-197">請注意該 hello 模型包含兩個資料事件：**溫度**和**溼度**。</span><span class="sxs-lookup"><span data-stu-id="4b851-197">Note that hello model includes two data events: **Temperature** and **Humidity**.</span></span> <span data-ttu-id="4b851-198">不同於上述範例中，每個事件 hello 類型是定義使用的結構**DECLARE\_結構**。</span><span class="sxs-lookup"><span data-stu-id="4b851-198">Unlike previous examples, hello type of each event is a structure defined using **DECLARE\_STRUCT**.</span></span> <span data-ttu-id="4b851-199">**TemperatureEvent** 包含溫度測量和時間戳記；**HumidityEvent** 包含溼度測量和時間戳記。</span><span class="sxs-lookup"><span data-stu-id="4b851-199">**TemperatureEvent** includes a temperature measurement and a timestamp; **HumidityEvent** contains a humidity measurement and a timestamp.</span></span> <span data-ttu-id="4b851-200">此模型會提供自然的方式 toomodel hello 資料 hello 上面所述的案例。</span><span class="sxs-lookup"><span data-stu-id="4b851-200">This model gives us a natural way toomodel hello data for hello scenario described above.</span></span> <span data-ttu-id="4b851-201">當我們傳送事件 toohello 雲端時，我們可能會傳送溫度/時間戳記或時間戳記溼度/配對。</span><span class="sxs-lookup"><span data-stu-id="4b851-201">When we send an event toohello cloud, we'll either send a temperature/timestamp or a humidity/timestamp pair.</span></span>

<span data-ttu-id="4b851-202">我們可以傳送溫度事件 toohello 雲端中使用 hello 如下的程式碼：</span><span class="sxs-lookup"><span data-stu-id="4b851-202">We can send a temperature event toohello cloud using code such as hello following:</span></span>

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

<span data-ttu-id="4b851-203">我們會使用硬式編碼值氣溫和溼度 hello 範例程式碼，但假設，我們實際擷取這些值由取樣 hello hello thermostat 上的對應感應器。</span><span class="sxs-lookup"><span data-stu-id="4b851-203">We'll use hard-coded values for temperature and humidity in hello sample code, but imagine that we’re actually retrieving these values by sampling hello corresponding sensors on hello thermostat.</span></span>

<span data-ttu-id="4b851-204">hello 上述的程式碼會使用 hello **GetDateTimeOffset**引進了先前的協助程式。</span><span class="sxs-lookup"><span data-stu-id="4b851-204">hello code above uses hello **GetDateTimeOffset** helper that was introduced previously.</span></span> <span data-ttu-id="4b851-205">原因將會清除更新版本，此程式碼明確分隔 hello 的工作序列化，以及傳送嗨事件。</span><span class="sxs-lookup"><span data-stu-id="4b851-205">For reasons that will become clear later, this code explicitly separates hello task of serializing and sending hello event.</span></span> <span data-ttu-id="4b851-206">hello 先前的程式碼會將 hello 溫度事件序列化至緩衝區。</span><span class="sxs-lookup"><span data-stu-id="4b851-206">hello previous code serializes hello temperature event into a buffer.</span></span> <span data-ttu-id="4b851-207">然後， **sendMessage**是 helper 函式 (包含在**simplesample\_amqp**) 傳送 hello 事件 tooIoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="4b851-207">Then, **sendMessage** is a helper function (included in **simplesample\_amqp**) that sends hello event tooIoT Hub:</span></span>

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

<span data-ttu-id="4b851-208">此程式碼是子集 hello **SendAsync** helper hello 上一節中所述，因此我們將不會在這裡透過它一次。</span><span class="sxs-lookup"><span data-stu-id="4b851-208">This code is a subset of hello **SendAsync** helper described in hello previous section, so we won’t go over it again here.</span></span>

<span data-ttu-id="4b851-209">當我們執行 hello 先前程式碼 toosend hello 溫度的事件時，這種 hello 事件序列化的形式傳送 tooIoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="4b851-209">When we run hello previous code toosend hello Temperature event, this serialized form of hello event is sent tooIoT Hub:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="4b851-210">我們要傳送的溫度屬於 **TemperatureEvent** 類型，而該結構包含 **Temperature** 和 **Time** 成員。</span><span class="sxs-lookup"><span data-stu-id="4b851-210">We're sending a temperature which is of type **TemperatureEvent** and that struct contains a **Temperature** and **Time** member.</span></span> <span data-ttu-id="4b851-211">這會直接反映 hello 序列化資料中。</span><span class="sxs-lookup"><span data-stu-id="4b851-211">This is directly reflected in hello serialized data.</span></span>

<span data-ttu-id="4b851-212">同樣地，我們可以利用此程式碼來傳送溼度事件：</span><span class="sxs-lookup"><span data-stu-id="4b851-212">Similarly, we can send a humidity event with this code:</span></span>

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="4b851-213">傳送 tooIoT 中樞 hello 序列化表單隨即出現，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4b851-213">hello serialized form that’s sent tooIoT Hub appears as follows:</span></span>

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="4b851-214">同樣地，全如預期一般。</span><span class="sxs-lookup"><span data-stu-id="4b851-214">Again, this is as expected.</span></span>

<span data-ttu-id="4b851-215">您可以使用此模型來想像如何輕鬆地加入其他事件。</span><span class="sxs-lookup"><span data-stu-id="4b851-215">With this model, you can imagine how additional events can easily be added.</span></span> <span data-ttu-id="4b851-216">您定義使用多個結構**DECLARE\_結構**，並將 hello 對應事件包含在 hello 模型使用**WITH\_資料**。</span><span class="sxs-lookup"><span data-stu-id="4b851-216">You define more structures using **DECLARE\_STRUCT**, and include hello corresponding event in hello model using **WITH\_DATA**.</span></span>

<span data-ttu-id="4b851-217">現在，讓我們來修改 hello 模型，使其包含 hello 相同的資料，但不同的結構。</span><span class="sxs-lookup"><span data-stu-id="4b851-217">Now, let’s modify hello model so that it includes hello same data but with a different structure.</span></span>

### <a name="model-2"></a><span data-ttu-id="4b851-218">模型 2</span><span class="sxs-lookup"><span data-stu-id="4b851-218">Model 2</span></span>
<span data-ttu-id="4b851-219">上方，請考慮這個替代的模型 toohello 其中一個：</span><span class="sxs-lookup"><span data-stu-id="4b851-219">Consider this alternative model toohello one above:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="4b851-220">在此情況下，我們已去除 hello **DECLARE\_結構**巨集，只會定義從我們的案例中使用簡單型別從模組化語言 hello hello 資料項目。</span><span class="sxs-lookup"><span data-stu-id="4b851-220">In this case we've eliminated hello **DECLARE\_STRUCT** macros and are simply defining hello data items from our scenario using simple types from hello modeling language.</span></span>

<span data-ttu-id="4b851-221">只針對 hello 目前我們忽略 hello**時間**事件。</span><span class="sxs-lookup"><span data-stu-id="4b851-221">Just for hello moment let’s ignore hello **Time** event.</span></span> <span data-ttu-id="4b851-222">與該另行，以下是 hello 程式碼 tooingress**溫度**:</span><span class="sxs-lookup"><span data-stu-id="4b851-222">With that aside, here’s hello code tooingress **Temperature**:</span></span>

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

<span data-ttu-id="4b851-223">此程式碼會傳送 hello 下列序列化事件 tooIoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="4b851-223">This code sends hello following serialized event tooIoT Hub:</span></span>

```
{"Temperature":75}
```

<span data-ttu-id="4b851-224">而且 hello 傳送 hello 溼度事件程式碼會出現，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4b851-224">And hello code for sending hello Humidity event appears as follows:</span></span>

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="4b851-225">此程式碼會傳送此 tooIoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="4b851-225">This code sends this tooIoT Hub:</span></span>

```
{"Humidity":45}
```

<span data-ttu-id="4b851-226">到目前為止，仍毫無意外。</span><span class="sxs-lookup"><span data-stu-id="4b851-226">So far there are still no surprises.</span></span> <span data-ttu-id="4b851-227">現在我們來變更 我們如何使用 hello 序列化巨集。</span><span class="sxs-lookup"><span data-stu-id="4b851-227">Now let's change how we use hello SERIALIZE macro.</span></span>

<span data-ttu-id="4b851-228">hello**序列化**巨集可做為引數的多個資料事件。</span><span class="sxs-lookup"><span data-stu-id="4b851-228">hello **SERIALIZE** macro can take multiple data events as arguments.</span></span> <span data-ttu-id="4b851-229">這可讓我們 tooserialize hello**溫度**和**溼度**事件放在一起，並在單一呼叫中傳送 tooIoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="4b851-229">This enables us tooserialize hello **Temperature** and **Humidity** event together and send them tooIoT Hub in one call:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="4b851-230">您猜的這段程式碼的 hello 結果是兩個資料事件會傳送 tooIoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="4b851-230">You might guess that hello result of this code is that two data events are sent tooIoT Hub:</span></span>

<span data-ttu-id="4b851-231">[</span><span class="sxs-lookup"><span data-stu-id="4b851-231">[</span></span>

<span data-ttu-id="4b851-232">{"Temperature":75},</span><span class="sxs-lookup"><span data-stu-id="4b851-232">{"Temperature":75},</span></span>

<span data-ttu-id="4b851-233">{"Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="4b851-233">{"Humidity":45}</span></span>

<span data-ttu-id="4b851-234">]</span><span class="sxs-lookup"><span data-stu-id="4b851-234">]</span></span>

<span data-ttu-id="4b851-235">換句話說，您可能預期這段程式碼是 hello 相同傳送**溫度**和**溼度**分開。</span><span class="sxs-lookup"><span data-stu-id="4b851-235">In other words, you might expect that this code is hello same as sending **Temperature** and **Humidity** separately.</span></span> <span data-ttu-id="4b851-236">它是只方便 toopass 這兩個事件太**序列化**hello 在相同呼叫。</span><span class="sxs-lookup"><span data-stu-id="4b851-236">It’s just a convenience toopass both events too**SERIALIZE** in hello same call.</span></span> <span data-ttu-id="4b851-237">不過，這不是 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="4b851-237">However, that’s not hello case.</span></span> <span data-ttu-id="4b851-238">相反地，hello 上述的程式碼會傳送這個單一資料事件 tooIoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="4b851-238">Instead, hello code above sends this single data event tooIoT Hub:</span></span>

<span data-ttu-id="4b851-239">{"Temperature":75, "Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="4b851-239">{"Temperature":75, "Humidity":45}</span></span>

<span data-ttu-id="4b851-240">這可能看似奇怪，因為我們的模型將 **Temperature** 和 **Humidity** 定義成兩個「個別」事件：</span><span class="sxs-lookup"><span data-stu-id="4b851-240">This may seem strange because our model defines **Temperature** and **Humidity** as two *separate* events:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="4b851-241">多個 toohello 點，我們沒有這些事件模型其中**溫度**和**溼度**hello 中相同的結構：</span><span class="sxs-lookup"><span data-stu-id="4b851-241">More toohello point, we didn’t model these events where **Temperature** and **Humidity** are in hello same structure:</span></span>

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

<span data-ttu-id="4b851-242">如果我們使用此模型時，將更容易 toounderstand 如何**溫度**和**溼度**就會傳送 hello 中相同序列化訊息。</span><span class="sxs-lookup"><span data-stu-id="4b851-242">If we used this model, it would be easier toounderstand how **Temperature** and **Humidity** would be sent in hello same serialized message.</span></span> <span data-ttu-id="4b851-243">不過它可能無法清除為什麼 ﹐，這樣一來當您將傳遞這兩個資料事件太**序列化**使用模型 2。</span><span class="sxs-lookup"><span data-stu-id="4b851-243">However it may not be clear why it works that way when you pass both data events too**SERIALIZE** using model 2.</span></span>

<span data-ttu-id="4b851-244">如果您知道該 hello hello 假設，此行為是更容易 toounderstand**序列化程式**正在程式庫。</span><span class="sxs-lookup"><span data-stu-id="4b851-244">This behavior is easier toounderstand if you know hello assumptions that hello **serializer** library is making.</span></span> <span data-ttu-id="4b851-245">toomake 意義吧後 tooour 模型：</span><span class="sxs-lookup"><span data-stu-id="4b851-245">toomake sense of this let’s go back tooour model:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="4b851-246">請以物件導向的觀點思考此模型。</span><span class="sxs-lookup"><span data-stu-id="4b851-246">Think of this model in object-oriented terms.</span></span> <span data-ttu-id="4b851-247">在此案例中，我們要模型化的是一個實體裝置 (控溫器)，而該裝置包含 **Temperature** 和 **Humidity** 之類的屬性。</span><span class="sxs-lookup"><span data-stu-id="4b851-247">In this case we’re modeling a physical device (a thermostat) and that device includes attributes like **Temperature** and **Humidity**.</span></span>

<span data-ttu-id="4b851-248">我們可以傳送 hello 與 hello 如下的程式碼模型的完整的狀態：</span><span class="sxs-lookup"><span data-stu-id="4b851-248">We can send hello entire state of our model with code such as hello following:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="4b851-249">假設 hello 值溫度、 溼度和時間設定，我們將會看到類似此傳送 tooIoT 中樞事件：</span><span class="sxs-lookup"><span data-stu-id="4b851-249">Assuming hello values of Temperature, Humidity and Time are set, we would see an event like this sent tooIoT Hub:</span></span>

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="4b851-250">有時候您可能只想 toosend*某些*hello 模型 toohello 雲端 （特別是如果您的模型包含大量的資料事件） 的內容。</span><span class="sxs-lookup"><span data-stu-id="4b851-250">Sometimes you may only want toosend *some* properties of hello model toohello cloud (this is especially true if your model contains a large number of data events).</span></span> <span data-ttu-id="4b851-251">它是有用 toosend 子集的資料事件，如在先前的範例：</span><span class="sxs-lookup"><span data-stu-id="4b851-251">It’s useful toosend only a subset of data events, such as in our earlier example:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="4b851-252">這會產生完全 hello 相同序列化事件，如同我們已經定義**TemperatureEvent**與**溫度**和**時間**成員，就像我們並未與模型 1。</span><span class="sxs-lookup"><span data-stu-id="4b851-252">This generates exactly hello same serialized event as if we had defined a **TemperatureEvent** with a **Temperature** and **Time** member, just as we did with model 1.</span></span> <span data-ttu-id="4b851-253">我們在此情況下無法 toogenerate 完全 hello 相同序列化事件使用不同的模型 （模型 2），因為我們呼叫**序列化**以不同方式。</span><span class="sxs-lookup"><span data-stu-id="4b851-253">In this case we were able toogenerate exactly hello same serialized event by using a different model (model 2) because we called **SERIALIZE** in a different way.</span></span>

<span data-ttu-id="4b851-254">hello 很重要的一點是，如果您傳遞太多個資料事件**序列化，**然後它會假設每個事件位於單一 JSON 物件中的屬性。</span><span class="sxs-lookup"><span data-stu-id="4b851-254">hello important point is that if you pass multiple data events too**SERIALIZE,** then it assumes each event is a property in a single JSON object.</span></span>

<span data-ttu-id="4b851-255">hello 最好的方法取決於您和考慮您的模型。</span><span class="sxs-lookup"><span data-stu-id="4b851-255">hello best approach depends on you and how you think about your model.</span></span> <span data-ttu-id="4b851-256">如果您要傳送 「 事件 」 toohello 雲端，而且每個事件包含一組定義的屬性，hello 第一種方法可讓一個很實用。</span><span class="sxs-lookup"><span data-stu-id="4b851-256">If you’re sending "events" toohello cloud and each event contains a defined set of properties, then hello first approach makes a lot of sense.</span></span> <span data-ttu-id="4b851-257">在此情況下，您會使用**DECLARE\_結構**toodefine hello 結構的每個事件，然後將它們包含在您的模型，以 hello **WITH\_資料**巨集。</span><span class="sxs-lookup"><span data-stu-id="4b851-257">In that case you would use **DECLARE\_STRUCT** toodefine hello structure of each event and then include them in your model with hello **WITH\_DATA** macro.</span></span> <span data-ttu-id="4b851-258">然後可以如同我們在 hello 上面的第一個範例中傳送的每個事件。</span><span class="sxs-lookup"><span data-stu-id="4b851-258">Then you send each event as we did in hello first example above.</span></span> <span data-ttu-id="4b851-259">在這種方法中您可以只傳遞單一的資料事件太**序列化程式**。</span><span class="sxs-lookup"><span data-stu-id="4b851-259">In this approach you would only pass a single data event too**SERIALIZER**.</span></span>

<span data-ttu-id="4b851-260">如果您認為有關您的模型物件導向的方式，然後 hello 第二種方法可能適合您。</span><span class="sxs-lookup"><span data-stu-id="4b851-260">If you think about your model in an object-oriented fashion, then hello second approach may suit you.</span></span> <span data-ttu-id="4b851-261">在此情況下，hello 定義使用的項目**WITH\_資料**是 hello 「 屬性 」 的物件。</span><span class="sxs-lookup"><span data-stu-id="4b851-261">In this case, hello elements defined using **WITH\_DATA** are hello "properties" of your object.</span></span> <span data-ttu-id="4b851-262">您傳遞事件的任何子集太**序列化**，您想要根據您 「 物件 」 狀態中有多少 toosend toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="4b851-262">You pass whatever subset of events too**SERIALIZE** that you like, depending on how much of your "object’s" state you want toosend toohello cloud.</span></span>

<span data-ttu-id="4b851-263">沒有絕對正確或錯誤的方法。</span><span class="sxs-lookup"><span data-stu-id="4b851-263">Nether approach is right or wrong.</span></span> <span data-ttu-id="4b851-264">只是如何 hello**序列化程式**程式庫的運作方式，並挑選 hello 模型化方法最適合您的需求。</span><span class="sxs-lookup"><span data-stu-id="4b851-264">Just be aware of how hello **serializer** library works, and pick hello modeling approach that best fits your needs.</span></span>

## <a name="message-handling"></a><span data-ttu-id="4b851-265">訊息處理</span><span class="sxs-lookup"><span data-stu-id="4b851-265">Message handling</span></span>
<span data-ttu-id="4b851-266">到目前為止本文僅討論傳送事件 tooIoT 集線器，，而且尚未處理接收訊息。</span><span class="sxs-lookup"><span data-stu-id="4b851-266">So far this article has only discussed sending events tooIoT Hub, and hasn't addressed receiving messages.</span></span> <span data-ttu-id="4b851-267">hello 原因 tooknow 關於接收訊息為此，我們需要主要中涵蓋[稍早文章](iot-hub-device-sdk-c-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="4b851-267">hello reason for this is that what we need tooknow about receiving messages has largely been covered in an [earlier article](iot-hub-device-sdk-c-intro.md).</span></span> <span data-ttu-id="4b851-268">請從那篇文章回憶，您是藉由註冊訊息回呼函式來處理訊息：</span><span class="sxs-lookup"><span data-stu-id="4b851-268">Recall from that article that you process messages by registering a message callback function:</span></span>

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

<span data-ttu-id="4b851-269">接著，您可以撰寫在 hello 時收到訊息時叫用的回呼函式：</span><span class="sxs-lookup"><span data-stu-id="4b851-269">You then write hello callback function that’s invoked when a message is received:</span></span>

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

<span data-ttu-id="4b851-270">這項實作**IoTHubMessage**呼叫 hello 您的模型中每個動作的特定函式。</span><span class="sxs-lookup"><span data-stu-id="4b851-270">This implementation of **IoTHubMessage** calls hello specific function for each action in your model.</span></span> <span data-ttu-id="4b851-271">例如，如果您的模型定義這項動作：</span><span class="sxs-lookup"><span data-stu-id="4b851-271">For example, if your model defines this action:</span></span>

```
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="4b851-272">您必須使用此簽章定義函式：</span><span class="sxs-lookup"><span data-stu-id="4b851-272">You must define a function with this signature:</span></span>

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="4b851-273">**SetAirResistance** tooyour 裝置傳送該訊息時再呼叫。</span><span class="sxs-lookup"><span data-stu-id="4b851-273">**SetAirResistance** is then called when that message is sent tooyour device.</span></span>

<span data-ttu-id="4b851-274">我們還沒說明尚未的訊息看起來像是 hello 序列化版本。</span><span class="sxs-lookup"><span data-stu-id="4b851-274">What we haven't explained yet is what hello serialized version of message looks like.</span></span> <span data-ttu-id="4b851-275">換句話說，如果您想 toosend **SetAirResistance**訊息 tooyour 裝置，該的外觀為何？</span><span class="sxs-lookup"><span data-stu-id="4b851-275">In other words, if you want toosend a **SetAirResistance** message tooyour device, what does that look like?</span></span>

<span data-ttu-id="4b851-276">如果您要傳送的訊息 tooa 裝置，您會達成透過 hello Azure IoT 服務 SDK。</span><span class="sxs-lookup"><span data-stu-id="4b851-276">If you're sending a message tooa device, you would do so through hello Azure IoT service SDK.</span></span> <span data-ttu-id="4b851-277">您需要 tooknow 字串 toosend tooinvoke 特定動作。</span><span class="sxs-lookup"><span data-stu-id="4b851-277">You still need tooknow what string toosend tooinvoke a particular action.</span></span> <span data-ttu-id="4b851-278">hello 傳送訊息的一般格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="4b851-278">hello general format for sending a message appears as follows:</span></span>

```
{"Name" : "", "Parameters" : "" }
```

<span data-ttu-id="4b851-279">您要傳送序列化的 JSON 物件，使用兩個屬性：**名稱**hello 名稱 hello 動作 （訊息） 和**參數**包含 hello 參數，該動作。</span><span class="sxs-lookup"><span data-stu-id="4b851-279">You're sending a serialized JSON object with two properties: **Name** is hello name of hello action (message) and **Parameters** contains hello parameters of that action.</span></span>

<span data-ttu-id="4b851-280">例如，tooinvoke **SetAirResistance**可以傳送此訊息 tooa 裝置：</span><span class="sxs-lookup"><span data-stu-id="4b851-280">For example, tooinvoke **SetAirResistance** you can send this message tooa device:</span></span>

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

<span data-ttu-id="4b851-281">hello 動作名稱必須完全符合您的模型中定義的動作。</span><span class="sxs-lookup"><span data-stu-id="4b851-281">hello action name must exactly match an action defined in your model.</span></span> <span data-ttu-id="4b851-282">必須同時符合 hello 參數名稱。</span><span class="sxs-lookup"><span data-stu-id="4b851-282">hello parameter names must match as well.</span></span> <span data-ttu-id="4b851-283">也請注意區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="4b851-283">Also note case sensitivity.</span></span> <span data-ttu-id="4b851-284">**Name** 和 **Parameters** 一律是大寫。</span><span class="sxs-lookup"><span data-stu-id="4b851-284">**Name** and **Parameters** are always uppercase.</span></span> <span data-ttu-id="4b851-285">在模型中，請確定 toomatch hello 情況下，您的動作名稱和參數。</span><span class="sxs-lookup"><span data-stu-id="4b851-285">Make sure toomatch hello case of your action name and parameters in your model.</span></span> <span data-ttu-id="4b851-286">在此範例中，hello 動作名稱是"SetAirResistance"並不是"setairresistance"。</span><span class="sxs-lookup"><span data-stu-id="4b851-286">In this example, hello action name is "SetAirResistance" and not "setairresistance".</span></span>

<span data-ttu-id="4b851-287">hello 其他兩個動作**TurnFanOn**和**TurnFanOff**可以傳送這些訊息 tooa 裝置叫用：</span><span class="sxs-lookup"><span data-stu-id="4b851-287">hello two other actions **TurnFanOn** and **TurnFanOff** can be invoked by sending these messages tooa device:</span></span>

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

<span data-ttu-id="4b851-288">本章節所述的一切 tooknow 時將事件傳送和接收訊息與 hello**序列化程式**程式庫。</span><span class="sxs-lookup"><span data-stu-id="4b851-288">This section described everything you need tooknow when sending events and receiving messages with hello **serializer** library.</span></span> <span data-ttu-id="4b851-289">在繼續討論之前，讓我們先討論一些您可以設定以控制模型大小的參數。</span><span class="sxs-lookup"><span data-stu-id="4b851-289">Before moving on, let's cover some parameters you can configure that control how large your model is.</span></span>

## <a name="macro-configuration"></a><span data-ttu-id="4b851-290">巨集組態</span><span class="sxs-lookup"><span data-stu-id="4b851-290">Macro configuration</span></span>
<span data-ttu-id="4b851-291">如果您使用 hello**序列化程式**hello azure-c-共用-公用程式程式庫中找到 hello SDK toobe 注意的重要部分的程式庫。</span><span class="sxs-lookup"><span data-stu-id="4b851-291">If you’re using hello **Serializer** library an important part of hello SDK toobe aware of is found in hello azure-c-shared-utility library.</span></span>
<span data-ttu-id="4b851-292">如果您已經複製 hello Azure iot-sdk c 儲存機制從 GitHub 使用 hello-遞迴 選項，您會找到這個公用程式共用程式庫：</span><span class="sxs-lookup"><span data-stu-id="4b851-292">If you have cloned hello Azure-iot-sdk-c repository from GitHub using hello --recursive option, then you will find this shared utility library here:</span></span>

```
.\\c-utility
```

<span data-ttu-id="4b851-293">如果您已經不複製 hello 程式庫，您可以找到[這裡](https://github.com/Azure/azure-c-shared-utility)。</span><span class="sxs-lookup"><span data-stu-id="4b851-293">If you have not cloned hello library, you can find it [here](https://github.com/Azure/azure-c-shared-utility).</span></span>

<span data-ttu-id="4b851-294">Hello 共用公用程式庫中，您將找到下列資料夾的 hello:</span><span class="sxs-lookup"><span data-stu-id="4b851-294">Within hello shared utility library, you will find hello following folder:</span></span>

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

<span data-ttu-id="4b851-295">此資料夾包含名為 **macro\_utils\_h\_generator.sln** 的 Visual Studio 方案：</span><span class="sxs-lookup"><span data-stu-id="4b851-295">This folder contains a Visual Studio solution called **macro\_utils\_h\_generator.sln**:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

<span data-ttu-id="4b851-296">在此解決方案中的 hello 程式會產生 hello**巨集\_utils.h**檔案。</span><span class="sxs-lookup"><span data-stu-id="4b851-296">hello program in this solution generates hello **macro\_utils.h** file.</span></span> <span data-ttu-id="4b851-297">沒有預設巨集\_utils.h hello SDK 所包含的檔案。</span><span class="sxs-lookup"><span data-stu-id="4b851-297">There’s a default macro\_utils.h file included with hello SDK.</span></span> <span data-ttu-id="4b851-298">此解決方案可讓您 toomodify 某些參數，然後重新建立 hello 根據這些參數的標頭檔。</span><span class="sxs-lookup"><span data-stu-id="4b851-298">This solution allows you toomodify some parameters and then recreate hello header file based on these parameters.</span></span>

<span data-ttu-id="4b851-299">hello 兩個索引鍵參數 toobe 關心**nArithmetic**和**nMacroParameters**巨集中找到這兩行定義所在\_utils.tt:</span><span class="sxs-lookup"><span data-stu-id="4b851-299">hello two key parameters toobe concerned with are **nArithmetic** and **nMacroParameters** which are defined in these two lines found in macro\_utils.tt:</span></span>

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

<span data-ttu-id="4b851-300">這些值為 hello hello SDK 所隨附的預設參數。</span><span class="sxs-lookup"><span data-stu-id="4b851-300">These values are hello default parameters included with hello SDK.</span></span> <span data-ttu-id="4b851-301">每個參數具有下列意義 hello:</span><span class="sxs-lookup"><span data-stu-id="4b851-301">Each parameter has hello following meaning:</span></span>

* <span data-ttu-id="4b851-302">nMacroParameters – 控制您在一個 DECLARE\_MODEL 巨集定義中可以擁有多少參數。</span><span class="sxs-lookup"><span data-stu-id="4b851-302">nMacroParameters – Controls how many parameters you can have in one DECLARE\_MODEL macro definition.</span></span>
* <span data-ttu-id="4b851-303">nArithmetic – 控制項 hello 的總數在模型中允許的成員。</span><span class="sxs-lookup"><span data-stu-id="4b851-303">nArithmetic – Controls hello total number of members allowed in a model.</span></span>

<span data-ttu-id="4b851-304">這些參數都是重要的 hello 原因是因為他們控制您的模型可以是多大。</span><span class="sxs-lookup"><span data-stu-id="4b851-304">hello reason these parameters are important is because they control how large your model can be.</span></span> <span data-ttu-id="4b851-305">例如，請考慮以此模型定義：</span><span class="sxs-lookup"><span data-stu-id="4b851-305">For example, consider this model definition:</span></span>

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

<span data-ttu-id="4b851-306">如先前所述，**DECLARE\_MODEL** 只是一個 C 巨集。</span><span class="sxs-lookup"><span data-stu-id="4b851-306">As mentioned previously, **DECLARE\_MODEL** is just a C macro.</span></span> <span data-ttu-id="4b851-307">hello hello 模型與 hello 名稱**WITH\_資料**陳述式 （但其他巨集） 是參數**DECLARE\_模型**。</span><span class="sxs-lookup"><span data-stu-id="4b851-307">hello names of hello model and hello **WITH\_DATA** statement (yet another macro) are parameters of **DECLARE\_MODEL**.</span></span> <span data-ttu-id="4b851-308">**nMacroParameters** 會定義 **DECLARE\_MODEL** 中可以包含多少參數。</span><span class="sxs-lookup"><span data-stu-id="4b851-308">**nMacroParameters** defines how many parameters can be included in **DECLARE\_MODEL**.</span></span> <span data-ttu-id="4b851-309">實際上，這定義的是您所能擁有的資料事件和動作宣告數目。</span><span class="sxs-lookup"><span data-stu-id="4b851-309">Effectively, this defines how many data event and action declarations you can have.</span></span> <span data-ttu-id="4b851-310">因此，124 hello 預設限制這表示您可以定義具有約 60 動作和事件資料的組合的模型。</span><span class="sxs-lookup"><span data-stu-id="4b851-310">As such, with hello default limit of 124 this means that you can define a model with a combination of about 60 actions and data events.</span></span> <span data-ttu-id="4b851-311">如果您嘗試 tooexceed 這項限制，您會收到看起來類似 toothis 編譯器錯誤：</span><span class="sxs-lookup"><span data-stu-id="4b851-311">If you try tooexceed this limit, you'll receive compiler errors that look similar toothis:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

<span data-ttu-id="4b851-312">hello **nArithmetic**參數是深入了解 hello 內部運作的 hello 巨集語言與您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4b851-312">hello **nArithmetic** parameter is more about hello internal workings of hello macro language than your application.</span></span>  <span data-ttu-id="4b851-313">它所控制的成員，您可以在模型中的 hello 總數包括**DECLARE_STRUCT**巨集。</span><span class="sxs-lookup"><span data-stu-id="4b851-313">It controls hello total number of members you can have in your model, including **DECLARE_STRUCT** macros.</span></span> <span data-ttu-id="4b851-314">如果您開始看到這類編譯器錯誤，則應該嘗試提高 **nArithmetic**的值：</span><span class="sxs-lookup"><span data-stu-id="4b851-314">If you start seeing compiler errors such as this, then you should try increasing **nArithmetic**:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

<span data-ttu-id="4b851-315">如果您想 toochange 這些參數，修改 hello 巨集中的 hello 值\_utils.tt 檔案、 重新編譯 hello 巨集\_utils\_h\_generator.sln 解決方案，以及執行的 hello 已編譯的程式。</span><span class="sxs-lookup"><span data-stu-id="4b851-315">If you want toochange these parameters, modify hello values in hello macro\_utils.tt file, recompile hello macro\_utils\_h\_generator.sln solution, and run hello compiled program.</span></span> <span data-ttu-id="4b851-316">當您這樣做，新的巨集\_utils.h 檔案會產生並放置於 hello。\\一般\\inc 目錄。</span><span class="sxs-lookup"><span data-stu-id="4b851-316">When you do so, a new macro\_utils.h file is generated and placed in hello .\\common\\inc directory.</span></span>

<span data-ttu-id="4b851-317">在巨集的順序 toouse hello 新版本\_utils.h、 移除 hello**序列化程式**NuGet 封裝，從您的方案，然後在其位置包含 hello**序列化程式**Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="4b851-317">In order toouse hello new version of macro\_utils.h, remove hello **serializer** NuGet package from your solution and in its place include hello **serializer** Visual Studio project.</span></span> <span data-ttu-id="4b851-318">這可讓您的程式碼 toocompile 針對 hello 序列化程式庫的 hello 原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="4b851-318">This enables your code toocompile against hello source code of hello serializer library.</span></span> <span data-ttu-id="4b851-319">這包括更新的 hello 巨集\_utils.h。</span><span class="sxs-lookup"><span data-stu-id="4b851-319">This includes hello updated macro\_utils.h.</span></span> <span data-ttu-id="4b851-320">如果您想 toodo 此作業對於**simplesample\_amqp**，開始移除 hello 方案中的 hello 序列化程式庫的 hello NuGet 封裝：</span><span class="sxs-lookup"><span data-stu-id="4b851-320">If you want toodo this for **simplesample\_amqp**, start by removing hello NuGet package for hello serializer library from hello solution:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

<span data-ttu-id="4b851-321">然後加入此專案 tooyour Visual Studio 方案：</span><span class="sxs-lookup"><span data-stu-id="4b851-321">Then add this project tooyour Visual Studio solution:</span></span>

> <span data-ttu-id="4b851-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span><span class="sxs-lookup"><span data-stu-id="4b851-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span></span>
> 
> 

<span data-ttu-id="4b851-323">完成時，解決方案應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="4b851-323">When you're done, your solution should look like this:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

<span data-ttu-id="4b851-324">現在當您編譯您的方案，hello 更新巨集\_utils.h 隨附於您的二進位檔。</span><span class="sxs-lookup"><span data-stu-id="4b851-324">Now when you compile your solution, hello updated macro\_utils.h is included in your binary.</span></span>

<span data-ttu-id="4b851-325">請注意，增加這些值到足夠高的數目可能會超出編譯器限制。</span><span class="sxs-lookup"><span data-stu-id="4b851-325">Note that increasing these values high enough can exceed compiler limits.</span></span> <span data-ttu-id="4b851-326">toothis 點，hello **nMacroParameters**是以 hello 擔心哪些 toobe 主要參數。</span><span class="sxs-lookup"><span data-stu-id="4b851-326">toothis point, hello **nMacroParameters** is hello main parameter with which toobe concerned.</span></span> <span data-ttu-id="4b851-327">hello C99 規格指定的巨集定義中允許有 127 參數的最小值。</span><span class="sxs-lookup"><span data-stu-id="4b851-327">hello C99 spec specifies that a minimum of 127 parameters are allowed in a macro definition.</span></span> <span data-ttu-id="4b851-328">hello Microsoft 編譯器完全遵循 hello 規格 （並已限制為 127），因此您必須能夠 tooincrease **nMacroParameters**超出 hello 預設。</span><span class="sxs-lookup"><span data-stu-id="4b851-328">hello Microsoft compiler follows hello spec exactly (and has a limit of 127), so you won't be able tooincrease **nMacroParameters** beyond hello default.</span></span> <span data-ttu-id="4b851-329">其他編譯器可讓您 toodo 因此 （例如，hello GNU 編譯器支援更高的限制）。</span><span class="sxs-lookup"><span data-stu-id="4b851-329">Other compilers might allow you toodo so (for example, hello GNU compiler supports a higher limit).</span></span>

<span data-ttu-id="4b851-330">到目前為止我們所討論的幾乎所需的一切相關 toowrite 撰寫程式碼以 hello tooknow**序列化程式**程式庫。</span><span class="sxs-lookup"><span data-stu-id="4b851-330">So far we've covered just about everything you need tooknow about how toowrite code with hello **serializer** library.</span></span> <span data-ttu-id="4b851-331">在做出結論之前，讓我們先從先前的文章中回顧一些您可能想知道的主題。</span><span class="sxs-lookup"><span data-stu-id="4b851-331">Before concluding, let's revisit some topics from previous articles that you may be wondering about.</span></span>

## <a name="hello-lower-level-apis"></a><span data-ttu-id="4b851-332">hello 較低層級應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="4b851-332">hello lower-level APIs</span></span>
<span data-ttu-id="4b851-333">這篇文章焦點所在的 hello 範例應用程式是**simplesample\_amqp**。</span><span class="sxs-lookup"><span data-stu-id="4b851-333">hello sample application on which this article focused is **simplesample\_amqp**.</span></span> <span data-ttu-id="4b851-334">此範例會使用 hello 較高層級 （hello 非-"LL"） 應用程式開發介面 toosend 事件，並接收訊息。</span><span class="sxs-lookup"><span data-stu-id="4b851-334">This sample uses hello higher-level (hello non-"LL") APIs toosend events and receive messages.</span></span> <span data-ttu-id="4b851-335">如果您使用這些 API，將會執行背景執行緒來處理事件傳送和訊息接收。</span><span class="sxs-lookup"><span data-stu-id="4b851-335">If you use these APIs, a background thread runs which takes care of both sending events and receiving messages.</span></span> <span data-ttu-id="4b851-336">不過，您可以使用 hello 較低層級 (LL) Api tooeliminate 這個背景執行緒，並採取明確控制當您將事件傳送或接收 hello 雲端中的訊息。</span><span class="sxs-lookup"><span data-stu-id="4b851-336">However, you can use hello lower-level (LL) APIs tooeliminate this background thread and take explicit control over when you send events or receive messages from hello cloud.</span></span>

<span data-ttu-id="4b851-337">中所述[前一篇文章](iot-hub-device-sdk-c-iothubclient.md)，沒有一組函式組成的 hello 較高層級的應用程式開發介面：</span><span class="sxs-lookup"><span data-stu-id="4b851-337">As described in a [previous article](iot-hub-device-sdk-c-iothubclient.md), there is a set of functions that consists of hello higher-level APIs:</span></span>

* <span data-ttu-id="4b851-338">IoTHubClient\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="4b851-338">IoTHubClient\_CreateFromConnectionString</span></span>
* <span data-ttu-id="4b851-339">IoTHubClient\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="4b851-339">IoTHubClient\_SendEventAsync</span></span>
* <span data-ttu-id="4b851-340">IoTHubClient\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="4b851-340">IoTHubClient\_SetMessageCallback</span></span>
* <span data-ttu-id="4b851-341">IoTHubClient\_Destroy</span><span class="sxs-lookup"><span data-stu-id="4b851-341">IoTHubClient\_Destroy</span></span>

<span data-ttu-id="4b851-342">**simplesample\_amqp** 中會示範這些 API。</span><span class="sxs-lookup"><span data-stu-id="4b851-342">These APIs are demonstrated in **simplesample\_amqp**.</span></span>

<span data-ttu-id="4b851-343">此外，也有一組類似的較低層級 API。</span><span class="sxs-lookup"><span data-stu-id="4b851-343">There is also an analogous set of lower-level APIs.</span></span>

* <span data-ttu-id="4b851-344">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="4b851-344">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="4b851-345">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="4b851-345">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="4b851-346">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="4b851-346">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="4b851-347">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="4b851-347">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="4b851-348">請注意，hello 較低層級 Api 工作完全 hello 相同方式與 hello 前一個發行項中所述。</span><span class="sxs-lookup"><span data-stu-id="4b851-348">Note that hello lower-level APIs work exactly hello same way as described in hello previous articles.</span></span> <span data-ttu-id="4b851-349">如果您想背景執行緒 toohandle 事件傳送和接收訊息，您可以使用 hello 第一組 Api。</span><span class="sxs-lookup"><span data-stu-id="4b851-349">You can use hello first set of APIs if you want a background thread toohandle sending events and receiving messages.</span></span> <span data-ttu-id="4b851-350">如果您想要明確控制當您傳送並接收來自 IoT 中樞的資料，您可以使用應用程式開發介面的 hello 第二個集合。</span><span class="sxs-lookup"><span data-stu-id="4b851-350">You use hello second set of APIs if you want explicit control over when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="4b851-351">設定的應用程式開發介面的工作也與 hello**序列化程式**程式庫。</span><span class="sxs-lookup"><span data-stu-id="4b851-351">Either set of APIs work equally well with hello **serializer** library.</span></span>

<span data-ttu-id="4b851-352">如需如何 hello 較低層級的 Api 來以 hello**序列化程式**程式庫，請參閱 hello **simplesample\_http**應用程式。</span><span class="sxs-lookup"><span data-stu-id="4b851-352">For an example of how hello lower-level APIs are used with hello **serializer** library, see hello **simplesample\_http** application.</span></span>

## <a name="additional-topics"></a><span data-ttu-id="4b851-353">其他主題</span><span class="sxs-lookup"><span data-stu-id="4b851-353">Additional topics</span></span>
<span data-ttu-id="4b851-354">幾個其他值得再次一提的主題包括屬性處理、使用替代裝置認證及組態選項。</span><span class="sxs-lookup"><span data-stu-id="4b851-354">A few other topics worth mentioning again are property handling, using alternate device credentials, and configuration options.</span></span> <span data-ttu-id="4b851-355">這些都是 [先前的文章](iot-hub-device-sdk-c-iothubclient.md)中所涵蓋的主題。</span><span class="sxs-lookup"><span data-stu-id="4b851-355">These are all topics covered in a [previous article](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="4b851-356">hello 重點是，所有這些功能的作用中 hello 相同方式與 hello**序列化程式**文件庫以 hello 一樣**IoTHubClient**程式庫。</span><span class="sxs-lookup"><span data-stu-id="4b851-356">hello main point is that all of these features work in hello same way with hello **serializer** library as they do with hello **IoTHubClient** library.</span></span> <span data-ttu-id="4b851-357">例如，如果您想 tooattach 屬性 tooan 事件從您的模型，您使用**IoTHubMessage\_屬性**和**對應**\_**AddorUpdate**，hello 相同方式就像先前所述：</span><span class="sxs-lookup"><span data-stu-id="4b851-357">For example, if you want tooattach properties tooan event from your model, you use **IoTHubMessage\_Properties** and **Map**\_**AddorUpdate**, hello same way as described previously:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="4b851-358">Hello 事件是否從 hello 產生**序列化程式**程式庫建立或手動使用 hello **IoTHubClient**程式庫並不重要。</span><span class="sxs-lookup"><span data-stu-id="4b851-358">Whether hello event was generated from hello **serializer** library or created manually using hello **IoTHubClient** library does not matter.</span></span>

<span data-ttu-id="4b851-359">Hello 交替使用的裝置認證**IoTHubClient\_LL\_建立**一樣能夠運作為**IoTHubClient\_CreateFromConnectionString**的配置**iot 中樞\_用戶端\_處理**。</span><span class="sxs-lookup"><span data-stu-id="4b851-359">For hello alternate device credentials, using **IoTHubClient\_LL\_Create** works just as well as **IoTHubClient\_CreateFromConnectionString** for allocating an **IOTHUB\_CLIENT\_HANDLE**.</span></span>

<span data-ttu-id="4b851-360">最後，如果您使用 hello**序列化程式**程式庫，您可以設定與組態選項**IoTHubClient\_LL\_SetOption**就像您未使用 hello時**IoTHubClient**程式庫。</span><span class="sxs-lookup"><span data-stu-id="4b851-360">Finally, if you're using hello **serializer** library, you can set configuration options with **IoTHubClient\_LL\_SetOption** just as you did when using hello **IoTHubClient** library.</span></span>

<span data-ttu-id="4b851-361">功能的唯一 toohello**序列化程式**文件庫中的 hello 初始化應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="4b851-361">A feature that is unique toohello **serializer** library are hello initialization APIs.</span></span> <span data-ttu-id="4b851-362">您可以開始使用 hello 程式庫之前，必須先呼叫**序列化程式\_init**:</span><span class="sxs-lookup"><span data-stu-id="4b851-362">Before you can start working with hello library, you must call **serializer\_init**:</span></span>

```
serializer_init(NULL);
```

<span data-ttu-id="4b851-363">此動作必須正好在呼叫 **IoTHubClient\_CreateFromConnectionString** 之前執行。</span><span class="sxs-lookup"><span data-stu-id="4b851-363">This is done just before you call **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="4b851-364">同樣地，當您完成使用 hello 程式庫，您要進行的 hello 最後一次呼叫太**序列化程式\_deinit**:</span><span class="sxs-lookup"><span data-stu-id="4b851-364">Similarly, when you're done working with hello library, hello last call you’ll make is too**serializer\_deinit**:</span></span>

```
serializer_deinit();
```

<span data-ttu-id="4b851-365">否則，所有的 hello 上面所列的其他功能工作相同的 hello hello**序列化程式**程式庫在 hello **IoTHubClient**程式庫。</span><span class="sxs-lookup"><span data-stu-id="4b851-365">Otherwise, all of hello other features listed above work hello same in hello **serializer** library as they do in hello **IoTHubClient** library.</span></span> <span data-ttu-id="4b851-366">如需這些主題的詳細資訊，請參閱 hello[前一篇文章](iot-hub-device-sdk-c-iothubclient.md)本系列。</span><span class="sxs-lookup"><span data-stu-id="4b851-366">For more information about any of these topics, see hello [previous article](iot-hub-device-sdk-c-iothubclient.md) in this series.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b851-367">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4b851-367">Next steps</span></span>
<span data-ttu-id="4b851-368">本文說明在詳細資料 hello 唯一的層面 hello**序列化程式**hello 中所包含的程式庫**C 的 Azure IoT 裝置 SDK**。提供的 hello 資訊應該充分了解如何 toouse 模型 toosend 事件也可以從 IoT 中心接收訊息。</span><span class="sxs-lookup"><span data-stu-id="4b851-368">This article describes in detail hello unique aspects of hello **serializer** library contained in hello **Azure IoT device SDK for C**. With hello information provided you should have a good understanding of how toouse models toosend events and receive messages from IoT Hub.</span></span>

<span data-ttu-id="4b851-369">這也會結束 hello 三部分的系列 toodevelop 應用程式如何 hello **C 的 Azure IoT 裝置 SDK**。這應該是您啟動足夠資訊的 toonot 只有 get，但可讓您瞭解 hello 應用程式開發介面的運作方式。</span><span class="sxs-lookup"><span data-stu-id="4b851-369">This also concludes hello three-part series on how toodevelop applications with hello **Azure IoT device SDK for C**. This should be enough information toonot only get you started but give you a thorough understanding of how hello APIs work.</span></span> <span data-ttu-id="4b851-370">如需詳細資訊，幾個範例中有 SDK 未涵蓋的 hello。</span><span class="sxs-lookup"><span data-stu-id="4b851-370">For additional information, there are a few samples in hello SDK not covered here.</span></span> <span data-ttu-id="4b851-371">否則，hello [SDK 文件](https://github.com/Azure/azure-iot-sdk-c)是很好的資源，如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="4b851-371">Otherwise, hello [SDK documentation](https://github.com/Azure/azure-iot-sdk-c) is a good resource for additional information.</span></span>

<span data-ttu-id="4b851-372">toolearn 進一步了解開發的 IoT 中樞，請參閱 hello [Azure IoT Sdk][lnk-sdks]。</span><span class="sxs-lookup"><span data-stu-id="4b851-372">toolearn more about developing for IoT Hub, see hello [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="4b851-373">toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：</span><span class="sxs-lookup"><span data-stu-id="4b851-373">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="4b851-374">[使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="4b851-374">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
