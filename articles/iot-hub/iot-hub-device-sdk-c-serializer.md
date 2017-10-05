---
title: "適用於 C 的 Azure IoT 裝置 SDK - 序列化程式 | Microsoft Docs"
description: "如何使用適用於 C 的 Azure IoT 裝置 SDK 中的 Serializer 程式庫，以建立與 IoT 中樞通訊的裝置應用程式。"
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
ms.openlocfilehash: aa03c29c54d75538b1fdf987cac5f09d5d344f73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a><span data-ttu-id="ed067-103">適用於 C 的 Azure IoT 裝置 SDK - 深入了解序列化程式</span><span class="sxs-lookup"><span data-stu-id="ed067-103">Azure IoT device SDK for C – more about serializer</span></span>
<span data-ttu-id="ed067-104">本系列的[第一篇文章](iot-hub-device-sdk-c-intro.md)介紹了「適用於 C 的 Azure IoT 裝置 SDK」。下一篇文章提供 [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md) 的更詳細描述。</span><span class="sxs-lookup"><span data-stu-id="ed067-104">The [first article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C**. The next article provided a more detailed description of the [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="ed067-105">本文將提供「序列化程式」  程式庫這個最後元件的更詳細描述，來完成 SDK 的涵蓋範圍。</span><span class="sxs-lookup"><span data-stu-id="ed067-105">This article completes coverage of the SDK by providing a more detailed description of the remaining component: the **serializer** library.</span></span>

<span data-ttu-id="ed067-106">本簡介文章描述如何使用「序列化程式」  程式庫將事件傳送至 IoT 中樞，以及接收來自 IoT 中樞的訊息。</span><span class="sxs-lookup"><span data-stu-id="ed067-106">The introductory article described how to use the **serializer** library to send events to and receive messages from IoT Hub.</span></span> <span data-ttu-id="ed067-107">在本文中，我們將更完整說明如何利用「序列化程式」  巨集語言來建立資料模型，以延伸該討論。</span><span class="sxs-lookup"><span data-stu-id="ed067-107">In this article, we extend that discussion by providing a more complete explanation of how to model your data with the **serializer** macro language.</span></span> <span data-ttu-id="ed067-108">本文也包含更多有關程式庫如何將訊息序列化 (以及在某些情況下，如何控制序列化行為) 的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ed067-108">The article also includes more detail about how the library serializes messages (and in some cases how you can control the serialization behavior).</span></span> <span data-ttu-id="ed067-109">我們也將描述您可以修改以判斷您所建立之模型大小的某些參數。</span><span class="sxs-lookup"><span data-stu-id="ed067-109">We'll also describe some parameters you can modify that determine the size of the models you create.</span></span>

<span data-ttu-id="ed067-110">最後，本文會回顧先前文章中涵蓋的一些主題，例如訊息和屬性處理。</span><span class="sxs-lookup"><span data-stu-id="ed067-110">Finally, the article revisits some topics covered in previous articles such as message and property handling.</span></span> <span data-ttu-id="ed067-111">因為我們將發現，使用「序列化程式」程式庫時，這些功能的運作方式與使用 **IoTHubClient** 程式庫時相同。</span><span class="sxs-lookup"><span data-stu-id="ed067-111">As we'll find out, those features work in the same way using the **serializer** library as they do with the **IoTHubClient** library.</span></span>

<span data-ttu-id="ed067-112">本文中描述的所有內容都是根據「序列化程式」SDK 範例。</span><span class="sxs-lookup"><span data-stu-id="ed067-112">Everything described in this article is based on the **serializer** SDK samples.</span></span> <span data-ttu-id="ed067-113">如果您想要依照這些內容，請參閱包含在「適用於 C 的 Azure IoT 裝置 SDK」中的 **simplesample\_amqp** 和 **simplesample\_http** 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed067-113">If you want to follow along, see the **simplesample\_amqp** and **simplesample\_http** applications included in the Azure IoT device SDK for C.</span></span>

<span data-ttu-id="ed067-114">您可以尋找[**適用於 C 的 Azure IoT 裝置 SDK**](https://github.com/Azure/azure-iot-sdk-c) GitHub 儲存機制，然後在 [C API 參考資料](https://azure.github.io/azure-iot-sdk-c/index.html)中檢視 API 的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ed067-114">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="the-modeling-language"></a><span data-ttu-id="ed067-115">模型化語言</span><span class="sxs-lookup"><span data-stu-id="ed067-115">The modeling language</span></span>
<span data-ttu-id="ed067-116">本系列中的[簡介文章](iot-hub-device-sdk-c-intro.md)透過 **simplesample\_amqp** 應用程式中提供的範例介紹了「適用於 C 的 Azure IoT 裝置 SDK」模型化語言：</span><span class="sxs-lookup"><span data-stu-id="ed067-116">The [introductory article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C** modeling language through the example provided in the **simplesample\_amqp** application:</span></span>

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

<span data-ttu-id="ed067-117">如您所見，模型化語言是以 C 巨集為基礎。</span><span class="sxs-lookup"><span data-stu-id="ed067-117">As you can see, the modeling language is based on C macros.</span></span> <span data-ttu-id="ed067-118">您的定義開頭一律會是 **BEGIN\_NAMESPACE**，而結尾則一律是 **END\_NAMESPACE**。</span><span class="sxs-lookup"><span data-stu-id="ed067-118">You always begin your definition with **BEGIN\_NAMESPACE** and always end with **END\_NAMESPACE**.</span></span> <span data-ttu-id="ed067-119">通常會為您的公司命名此命名空間，或如同此範例，為您正在使用的專案命名此命名空間。</span><span class="sxs-lookup"><span data-stu-id="ed067-119">It's common to name the namespace for your company or, as in this example, the project that you're working on.</span></span>

<span data-ttu-id="ed067-120">在命名空間內部進行的是模型定義。</span><span class="sxs-lookup"><span data-stu-id="ed067-120">What goes inside the namespace are model definitions.</span></span> <span data-ttu-id="ed067-121">在此案例中，有一個單一的風速計模型。</span><span class="sxs-lookup"><span data-stu-id="ed067-121">In this case, there is a single model for an anemometer.</span></span> <span data-ttu-id="ed067-122">同樣地，可以任意命名此模型，但通常會針對您想要與 IoT 中樞交換的裝置或資料類型來命名。</span><span class="sxs-lookup"><span data-stu-id="ed067-122">Once again, the model can be named anything, but typically this is named for the device or type of data you want to exchange with IoT Hub.</span></span>  

<span data-ttu-id="ed067-123">模型除了包含您可以從「IoT 中樞」接收的訊息 (動作) 之外，也包含您可以輸入到「IoT 中樞」(資料) 之事件的定義。</span><span class="sxs-lookup"><span data-stu-id="ed067-123">Models contain a definition of the events you can ingress to IoT Hub (the *data*) as well as the messages you can receive from IoT Hub (the *actions*).</span></span> <span data-ttu-id="ed067-124">如同您在範例中看到的，事件具有類型和名稱。動作會有一個名稱和選擇性的參數 (各有其類型)。</span><span class="sxs-lookup"><span data-stu-id="ed067-124">As you can see from the example, events have a type and a name; actions have a name and optional parameters (each with a type).</span></span>

<span data-ttu-id="ed067-125">此範例中並未示範 SDK 支援的其他資料類型。</span><span class="sxs-lookup"><span data-stu-id="ed067-125">What’s not demonstrated in this sample are additional data types that are supported by the SDK.</span></span> <span data-ttu-id="ed067-126">我們將在稍後討論。</span><span class="sxs-lookup"><span data-stu-id="ed067-126">We'll cover that next.</span></span>

> [!NOTE]
> <span data-ttu-id="ed067-127">「IoT 中樞」會將裝置傳送給它的資料視為「事件」，而模型化語言則是會將它視為「資料」(使用 **WITH_DATA** 來定義)。</span><span class="sxs-lookup"><span data-stu-id="ed067-127">IoT Hub refers to the data a device sends to it as *events*, while the modeling language refers to it as *data* (defined using **WITH_DATA**).</span></span> <span data-ttu-id="ed067-128">同樣地，「IoT 中樞」會將您傳送給裝置的資料視為「訊息」，而模型化語言則是會將它視為「動作」(使用 **WITH_ACTION** 來定義)。</span><span class="sxs-lookup"><span data-stu-id="ed067-128">Likewise, IoT Hub refers to the data you send to devices as *messages*, while the modeling language refers to it as *actions* (defined using **WITH_ACTION**).</span></span> <span data-ttu-id="ed067-129">請注意，在本文中可能會交替使用這些詞彙。</span><span class="sxs-lookup"><span data-stu-id="ed067-129">Be aware that these terms may be used interchangeably in this article.</span></span>
> 
> 

### <a name="supported-data-types"></a><span data-ttu-id="ed067-130">支援的資料類型</span><span class="sxs-lookup"><span data-stu-id="ed067-130">Supported data types</span></span>
<span data-ttu-id="ed067-131">利用 **序列化程式** 程式庫建立的模型支援下列資料類型：</span><span class="sxs-lookup"><span data-stu-id="ed067-131">The following data types are supported in models created with the **serializer** library:</span></span>

| <span data-ttu-id="ed067-132">類型</span><span class="sxs-lookup"><span data-stu-id="ed067-132">Type</span></span> | <span data-ttu-id="ed067-133">說明</span><span class="sxs-lookup"><span data-stu-id="ed067-133">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ed067-134">double</span><span class="sxs-lookup"><span data-stu-id="ed067-134">double</span></span> |<span data-ttu-id="ed067-135">雙精確度浮點數</span><span class="sxs-lookup"><span data-stu-id="ed067-135">double precision floating point number</span></span> |
| <span data-ttu-id="ed067-136">int</span><span class="sxs-lookup"><span data-stu-id="ed067-136">int</span></span> |<span data-ttu-id="ed067-137">32 位元整數</span><span class="sxs-lookup"><span data-stu-id="ed067-137">32 bit integer</span></span> |
| <span data-ttu-id="ed067-138">float</span><span class="sxs-lookup"><span data-stu-id="ed067-138">float</span></span> |<span data-ttu-id="ed067-139">單精確度浮點數</span><span class="sxs-lookup"><span data-stu-id="ed067-139">single precision floating point number</span></span> |
| <span data-ttu-id="ed067-140">long</span><span class="sxs-lookup"><span data-stu-id="ed067-140">long</span></span> |<span data-ttu-id="ed067-141">長整數</span><span class="sxs-lookup"><span data-stu-id="ed067-141">long integer</span></span> |
| <span data-ttu-id="ed067-142">int8\_t</span><span class="sxs-lookup"><span data-stu-id="ed067-142">int8\_t</span></span> |<span data-ttu-id="ed067-143">8 位元整數</span><span class="sxs-lookup"><span data-stu-id="ed067-143">8 bit integer</span></span> |
| <span data-ttu-id="ed067-144">int16\_t</span><span class="sxs-lookup"><span data-stu-id="ed067-144">int16\_t</span></span> |<span data-ttu-id="ed067-145">16 位元整數</span><span class="sxs-lookup"><span data-stu-id="ed067-145">16 bit integer</span></span> |
| <span data-ttu-id="ed067-146">int32\_t</span><span class="sxs-lookup"><span data-stu-id="ed067-146">int32\_t</span></span> |<span data-ttu-id="ed067-147">32 位元整數</span><span class="sxs-lookup"><span data-stu-id="ed067-147">32 bit integer</span></span> |
| <span data-ttu-id="ed067-148">int64\_t</span><span class="sxs-lookup"><span data-stu-id="ed067-148">int64\_t</span></span> |<span data-ttu-id="ed067-149">64 位元整數</span><span class="sxs-lookup"><span data-stu-id="ed067-149">64 bit integer</span></span> |
| <span data-ttu-id="ed067-150">布林</span><span class="sxs-lookup"><span data-stu-id="ed067-150">bool</span></span> |<span data-ttu-id="ed067-151">布林值</span><span class="sxs-lookup"><span data-stu-id="ed067-151">boolean</span></span> |
| <span data-ttu-id="ed067-152">ascii\_char\_ptr</span><span class="sxs-lookup"><span data-stu-id="ed067-152">ascii\_char\_ptr</span></span> |<span data-ttu-id="ed067-153">ASCII 字串</span><span class="sxs-lookup"><span data-stu-id="ed067-153">ASCII string</span></span> |
| <span data-ttu-id="ed067-154">EDM\_DATE\_TIME\_OFFSET</span><span class="sxs-lookup"><span data-stu-id="ed067-154">EDM\_DATE\_TIME\_OFFSET</span></span> |<span data-ttu-id="ed067-155">日期時間位移</span><span class="sxs-lookup"><span data-stu-id="ed067-155">date time offset</span></span> |
| <span data-ttu-id="ed067-156">EDM\_GUID</span><span class="sxs-lookup"><span data-stu-id="ed067-156">EDM\_GUID</span></span> |<span data-ttu-id="ed067-157">GUID</span><span class="sxs-lookup"><span data-stu-id="ed067-157">GUID</span></span> |
| <span data-ttu-id="ed067-158">EDM\_BINARY</span><span class="sxs-lookup"><span data-stu-id="ed067-158">EDM\_BINARY</span></span> |<span data-ttu-id="ed067-159">binary</span><span class="sxs-lookup"><span data-stu-id="ed067-159">binary</span></span> |
| <span data-ttu-id="ed067-160">DECLARE\_STRUCT</span><span class="sxs-lookup"><span data-stu-id="ed067-160">DECLARE\_STRUCT</span></span> |<span data-ttu-id="ed067-161">複雜資料類型</span><span class="sxs-lookup"><span data-stu-id="ed067-161">complex data type</span></span> |

<span data-ttu-id="ed067-162">我們先從最後一個資料類型開始討論。</span><span class="sxs-lookup"><span data-stu-id="ed067-162">Let’s start with the last data type.</span></span> <span data-ttu-id="ed067-163">**DECLARE\_STRUCT** 可讓您定義複雜的資料類型，也就是其他基本類型的群組。</span><span class="sxs-lookup"><span data-stu-id="ed067-163">The **DECLARE\_STRUCT** allows you to define complex data types, which are groupings of the other primitive types.</span></span> <span data-ttu-id="ed067-164">這些群組可讓我們定義看起來像這樣的模型：</span><span class="sxs-lookup"><span data-stu-id="ed067-164">These groupings allow us to define a model that looks like this:</span></span>

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

<span data-ttu-id="ed067-165">我們的模型包含 **TestType**類型的單一資料事件。</span><span class="sxs-lookup"><span data-stu-id="ed067-165">Our model contains a single data event of type **TestType**.</span></span> <span data-ttu-id="ed067-166">**TestType** 是包含數個成員的複雜類型，這些成員共同展示了「序列化程式」模型化語言所支援的基本類型。</span><span class="sxs-lookup"><span data-stu-id="ed067-166">**TestType** is a complex type that includes several members, which collectively demonstrate the primitive types supported by the **serializer** modeling language.</span></span>

<span data-ttu-id="ed067-167">使用類似這樣的模型，我們可以撰寫程式碼以將資料傳送到看起來像這樣的 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="ed067-167">With a model like this, we can write code to send data to IoT Hub that appears as follows:</span></span>

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

<span data-ttu-id="ed067-168">基本上，我們是將值指派給 **Test** 結構的每個成員，然後呼叫 **SendAsync** 將 **Test** 資料事件傳送到雲端。</span><span class="sxs-lookup"><span data-stu-id="ed067-168">Basically, we’re assigning a value to every member of the **Test** structure and then calling **SendAsync** to send the **Test** data event to the cloud.</span></span> <span data-ttu-id="ed067-169">**SendAsync** 是將單一資料事件傳送到 IoT 中樞的協助程式函式：</span><span class="sxs-lookup"><span data-stu-id="ed067-169">**SendAsync** is a helper function that sends a single data event to IoT Hub:</span></span>

```
void SendAsync(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const void *dataEvent)
{
    unsigned char* destination;
    size_t destinationSize;
    if (SERIALIZE(&destination, &destinationSize, *(const unsigned char*)dataEvent) ==
    {
        // null terminate the string
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

<span data-ttu-id="ed067-170">此函式會將指定的資料事件序列化，然後使用 **IoTHubClient\_SendEventAsync** 將它傳送到「IoT 中樞」。</span><span class="sxs-lookup"><span data-stu-id="ed067-170">This function serializes the given data event and sends it to IoT Hub using **IoTHubClient\_SendEventAsync**.</span></span> <span data-ttu-id="ed067-171">這是在先前的文章中討論過的相同程式碼 (**SendAsync** 會將邏輯封裝入方便的函式)。</span><span class="sxs-lookup"><span data-stu-id="ed067-171">This is the same code discussed in previous articles (**SendAsync** encapsulates the logic into a convenient function).</span></span>

<span data-ttu-id="ed067-172">在先前的程式碼中使用的一個其他協助程式函式是 **GetDateTimeOffset**。</span><span class="sxs-lookup"><span data-stu-id="ed067-172">One other helper function used in the previous code is **GetDateTimeOffset**.</span></span> <span data-ttu-id="ed067-173">此函式會將指定的時間轉換成 **EDM\_DATE\_TIME\_OFFSET** 類型的值：</span><span class="sxs-lookup"><span data-stu-id="ed067-173">This function transforms the given time into a value of type **EDM\_DATE\_TIME\_OFFSET**:</span></span>

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

<span data-ttu-id="ed067-174">如果您執行此程式碼，就會傳送下列訊息到 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="ed067-174">If you run this code, the following message is sent to IoT Hub:</span></span>

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

<span data-ttu-id="ed067-175">請注意，序列化是 JSON，這是 **序列化程式** 程式庫所產生的格式。</span><span class="sxs-lookup"><span data-stu-id="ed067-175">Note that the serialization is JSON, which is the format generated by the **serializer** library.</span></span> <span data-ttu-id="ed067-176">另請注意，序列化 JSON 物件的每個成員皆與在我們模型中定義的 **TestType** 成員相符。</span><span class="sxs-lookup"><span data-stu-id="ed067-176">Also note that each member of the serialized JSON object matches the members of the **TestType** that we defined in our model.</span></span> <span data-ttu-id="ed067-177">值也與程式碼中使用的值完全相符。</span><span class="sxs-lookup"><span data-stu-id="ed067-177">The values also exactly match those used in the code.</span></span> <span data-ttu-id="ed067-178">不過，請注意，二進位資料是採用 base64 編碼："AQID" 是 {0x01, 0x02, 0x03} 的 base64 編碼。</span><span class="sxs-lookup"><span data-stu-id="ed067-178">However, note that the binary data is base64-encoded: "AQID" is the base64 encoding of {0x01, 0x02, 0x03}.</span></span>

<span data-ttu-id="ed067-179">這個範例示範使用 **序列化程式** 程式庫的優點 -- 它可讓我們將 JSON 傳送至雲端，而不需要在我們的應用程式中明確處理序列化。</span><span class="sxs-lookup"><span data-stu-id="ed067-179">This example demonstrates the advantage of using the **serializer** library -- it enables us to send JSON to the cloud, without having to explicitly deal with serialization in our application.</span></span> <span data-ttu-id="ed067-180">我們所需操心的只有要在模型中設定資料事件的值，然後呼叫簡單的 API 將這些事件傳送至雲端。</span><span class="sxs-lookup"><span data-stu-id="ed067-180">All we have to worry about is setting the values of the data events in our model and then calling simple APIs to send those events to the cloud.</span></span>

<span data-ttu-id="ed067-181">有了這項資訊，我們便可以定義包含支援之資料類型範圍的模型，這些資料類型包括複雜類型 (我們甚至可以包含其他複雜類型內的複雜類型)。</span><span class="sxs-lookup"><span data-stu-id="ed067-181">With this information, we can define models that include the range of supported data types, including complex types (we could even include complex types within other complex types).</span></span> <span data-ttu-id="ed067-182">不過，上述範例所產生的序列化 JSON 突顯了一個重點。</span><span class="sxs-lookup"><span data-stu-id="ed067-182">However, he serialized JSON generated by the example above brings up an important point.</span></span> <span data-ttu-id="ed067-183">*如何* 利用  程式庫傳送資料，可完全決定 JSON 如何形成。</span><span class="sxs-lookup"><span data-stu-id="ed067-183">*How* we send data with the **serializer** library determines exactly how the JSON is formed.</span></span> <span data-ttu-id="ed067-184">此特點就是我們接下來要討論的內容。</span><span class="sxs-lookup"><span data-stu-id="ed067-184">That particular point is what we'll cover next.</span></span>

## <a name="more-about-serialization"></a><span data-ttu-id="ed067-185">深入了解序列化</span><span class="sxs-lookup"><span data-stu-id="ed067-185">More about serialization</span></span>
<span data-ttu-id="ed067-186">上一節強調 **序列化程式** 程式庫所產生的輸出範例。</span><span class="sxs-lookup"><span data-stu-id="ed067-186">The previous section highlights an example of the output generated by the **serializer** library.</span></span> <span data-ttu-id="ed067-187">在本節中，我們將說明程式庫如何將資料序列化，以及如何使用序列化 API 來控制該行為。</span><span class="sxs-lookup"><span data-stu-id="ed067-187">In this section, we'll explain how the library serializes data and how you can control that behavior using the serialization APIs.</span></span>

<span data-ttu-id="ed067-188">為了進一步討論序列化，我們將使用以控溫器為基礎的新模型。</span><span class="sxs-lookup"><span data-stu-id="ed067-188">In order to advance the discussion on serialization, we'll work with a new model based on a thermostat.</span></span> <span data-ttu-id="ed067-189">首先，讓我們針對所要嘗試處理的案例提供一些背景。</span><span class="sxs-lookup"><span data-stu-id="ed067-189">First, let's provide some background on the scenario we're trying to address.</span></span>

<span data-ttu-id="ed067-190">我們想要建立可測量氣溫和溼度的控溫器模型。</span><span class="sxs-lookup"><span data-stu-id="ed067-190">We want to model a thermostat that measures temperature and humidity.</span></span> <span data-ttu-id="ed067-191">每一項資料將會以不同的方式傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="ed067-191">Each piece of data is going to be sent to IoT Hub differently.</span></span> <span data-ttu-id="ed067-192">根據預設，控溫器會每 2 分鐘輸入溫度事件一次；每 15 分鐘輸入溼度事件一次。</span><span class="sxs-lookup"><span data-stu-id="ed067-192">By default, the thermostat ingresses a temperature event once every 2 minutes; a humidity event is ingressed once every 15 minutes.</span></span> <span data-ttu-id="ed067-193">輸入任一事件時，必須包含顯示相對應溫度或溼度之測量時間的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="ed067-193">When either event is ingressed, it must include a timestamp that shows the time that the corresponding temperature or humidity was measured.</span></span>

<span data-ttu-id="ed067-194">在這個案例中，我們將示範兩種不同的資料模型化方式，並將說明該模型化對序列化輸出的影響。</span><span class="sxs-lookup"><span data-stu-id="ed067-194">Given this scenario, we'll demonstrate two different ways to model the data, and we'll explain the effect that modeling has on the serialized output.</span></span>

### <a name="model-1"></a><span data-ttu-id="ed067-195">模型 1</span><span class="sxs-lookup"><span data-stu-id="ed067-195">Model 1</span></span>
<span data-ttu-id="ed067-196">以下是支援先前案例的第一版模型：</span><span class="sxs-lookup"><span data-stu-id="ed067-196">Here's the first version of a model that supports the previous scenario:</span></span>

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

<span data-ttu-id="ed067-197">請注意，此模型包含兩個資料事件：**Temperature** 和 **Humidity**。</span><span class="sxs-lookup"><span data-stu-id="ed067-197">Note that the model includes two data events: **Temperature** and **Humidity**.</span></span> <span data-ttu-id="ed067-198">與先前的範例不同，這裡每個事件的類型都是使用 **DECLARE\_STRUCT** 來定義的結構。</span><span class="sxs-lookup"><span data-stu-id="ed067-198">Unlike previous examples, the type of each event is a structure defined using **DECLARE\_STRUCT**.</span></span> <span data-ttu-id="ed067-199">**TemperatureEvent** 包含溫度測量和時間戳記；**HumidityEvent** 包含溼度測量和時間戳記。</span><span class="sxs-lookup"><span data-stu-id="ed067-199">**TemperatureEvent** includes a temperature measurement and a timestamp; **HumidityEvent** contains a humidity measurement and a timestamp.</span></span> <span data-ttu-id="ed067-200">此模型可讓我們以自然的方式模型化上述案例的資料。</span><span class="sxs-lookup"><span data-stu-id="ed067-200">This model gives us a natural way to model the data for the scenario described above.</span></span> <span data-ttu-id="ed067-201">當我們將事件傳送至雲端時，我們將會傳送溫度/時間戳記組或溼度/時間戳記組。</span><span class="sxs-lookup"><span data-stu-id="ed067-201">When we send an event to the cloud, we'll either send a temperature/timestamp or a humidity/timestamp pair.</span></span>

<span data-ttu-id="ed067-202">我們可以使用類似以下的程式碼將溫度事件傳送至雲端：</span><span class="sxs-lookup"><span data-stu-id="ed067-202">We can send a temperature event to the cloud using code such as the following:</span></span>

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

<span data-ttu-id="ed067-203">在範例程式碼中，我們將針對溫度和溼度使用硬式編碼值，但請想像成我們實際上是從控溫器上對應的感應器取樣來擷取這些值。</span><span class="sxs-lookup"><span data-stu-id="ed067-203">We'll use hard-coded values for temperature and humidity in the sample code, but imagine that we’re actually retrieving these values by sampling the corresponding sensors on the thermostat.</span></span>

<span data-ttu-id="ed067-204">上述程式碼使用先前介紹的協助程式 **GetDateTimeOffset** 。</span><span class="sxs-lookup"><span data-stu-id="ed067-204">The code above uses the **GetDateTimeOffset** helper that was introduced previously.</span></span> <span data-ttu-id="ed067-205">此程式碼會將序列化與傳送事件的工作明確分隔，原因在稍後會漸趨明朗。</span><span class="sxs-lookup"><span data-stu-id="ed067-205">For reasons that will become clear later, this code explicitly separates the task of serializing and sending the event.</span></span> <span data-ttu-id="ed067-206">先前的程式碼會將溫度事件以序列化方式傳送至緩衝區。</span><span class="sxs-lookup"><span data-stu-id="ed067-206">The previous code serializes the temperature event into a buffer.</span></span> <span data-ttu-id="ed067-207">然後，**sendMessage** 則是一個協助程式函式 (包含在 **simplesample\_amqp** 中)，會將事件傳送到「IoT 中樞」：</span><span class="sxs-lookup"><span data-stu-id="ed067-207">Then, **sendMessage** is a helper function (included in **simplesample\_amqp**) that sends the event to IoT Hub:</span></span>

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

<span data-ttu-id="ed067-208">此程式碼是前一節所述之 **SendAsync** 協助程式的子集，所以我們不會在此贅述。</span><span class="sxs-lookup"><span data-stu-id="ed067-208">This code is a subset of the **SendAsync** helper described in the previous section, so we won’t go over it again here.</span></span>

<span data-ttu-id="ed067-209">我們執行先前的程式碼以傳送溫度事件時，事件的序列化形式會傳送到 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="ed067-209">When we run the previous code to send the Temperature event, this serialized form of the event is sent to IoT Hub:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="ed067-210">我們要傳送的溫度屬於 **TemperatureEvent** 類型，而該結構包含 **Temperature** 和 **Time** 成員。</span><span class="sxs-lookup"><span data-stu-id="ed067-210">We're sending a temperature which is of type **TemperatureEvent** and that struct contains a **Temperature** and **Time** member.</span></span> <span data-ttu-id="ed067-211">這會直接反映在序列化資料中。</span><span class="sxs-lookup"><span data-stu-id="ed067-211">This is directly reflected in the serialized data.</span></span>

<span data-ttu-id="ed067-212">同樣地，我們可以利用此程式碼來傳送溼度事件：</span><span class="sxs-lookup"><span data-stu-id="ed067-212">Similarly, we can send a humidity event with this code:</span></span>

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="ed067-213">傳送到 IoT 中樞的序列化的形式如下所示：</span><span class="sxs-lookup"><span data-stu-id="ed067-213">The serialized form that’s sent to IoT Hub appears as follows:</span></span>

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="ed067-214">同樣地，全如預期一般。</span><span class="sxs-lookup"><span data-stu-id="ed067-214">Again, this is as expected.</span></span>

<span data-ttu-id="ed067-215">您可以使用此模型來想像如何輕鬆地加入其他事件。</span><span class="sxs-lookup"><span data-stu-id="ed067-215">With this model, you can imagine how additional events can easily be added.</span></span> <span data-ttu-id="ed067-216">您會使用 **DECLARE\_STRUCT** 來定義更多結構，並使用 **WITH\_DATA** 將相對應的事件包含在模型中。</span><span class="sxs-lookup"><span data-stu-id="ed067-216">You define more structures using **DECLARE\_STRUCT**, and include the corresponding event in the model using **WITH\_DATA**.</span></span>

<span data-ttu-id="ed067-217">現在，我們要修改模型，讓它包含相同的資料，但具有不同的結構。</span><span class="sxs-lookup"><span data-stu-id="ed067-217">Now, let’s modify the model so that it includes the same data but with a different structure.</span></span>

### <a name="model-2"></a><span data-ttu-id="ed067-218">模型 2</span><span class="sxs-lookup"><span data-stu-id="ed067-218">Model 2</span></span>
<span data-ttu-id="ed067-219">請考慮上述模型的替代模型：</span><span class="sxs-lookup"><span data-stu-id="ed067-219">Consider this alternative model to the one above:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="ed067-220">在此情況下，我們去除了 **DECLARE\_STRUCT** 巨集，而只使用來自模型化語言的簡單類型從我們的案例定義資料項目。</span><span class="sxs-lookup"><span data-stu-id="ed067-220">In this case we've eliminated the **DECLARE\_STRUCT** macros and are simply defining the data items from our scenario using simple types from the modeling language.</span></span>

<span data-ttu-id="ed067-221">現在讓我們忽略 **時間** 事件。</span><span class="sxs-lookup"><span data-stu-id="ed067-221">Just for the moment let’s ignore the **Time** event.</span></span> <span data-ttu-id="ed067-222">忽略該事件之後，以下是要輸入 **溫度**的程式碼：</span><span class="sxs-lookup"><span data-stu-id="ed067-222">With that aside, here’s the code to ingress **Temperature**:</span></span>

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

<span data-ttu-id="ed067-223">此程式碼會將下列序列化事件傳送到 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="ed067-223">This code sends the following serialized event to IoT Hub:</span></span>

```
{"Temperature":75}
```

<span data-ttu-id="ed067-224">而傳送 Humidity 事件的程式碼則看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="ed067-224">And the code for sending the Humidity event appears as follows:</span></span>

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="ed067-225">此程式碼會將其傳送至 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="ed067-225">This code sends this to IoT Hub:</span></span>

```
{"Humidity":45}
```

<span data-ttu-id="ed067-226">到目前為止，仍毫無意外。</span><span class="sxs-lookup"><span data-stu-id="ed067-226">So far there are still no surprises.</span></span> <span data-ttu-id="ed067-227">現在，讓我們變更 SERIALIZE 巨集的使用方式。</span><span class="sxs-lookup"><span data-stu-id="ed067-227">Now let's change how we use the SERIALIZE macro.</span></span>

<span data-ttu-id="ed067-228">**SERIALIZE** 巨集可以將多個資料事件視為引數。</span><span class="sxs-lookup"><span data-stu-id="ed067-228">The **SERIALIZE** macro can take multiple data events as arguments.</span></span> <span data-ttu-id="ed067-229">這可讓我們將 **Temperature** 與 **Humidity** 事件一起序列化，然後以單一呼叫將它們傳送到「IoT 中樞」：</span><span class="sxs-lookup"><span data-stu-id="ed067-229">This enables us to serialize the **Temperature** and **Humidity** event together and send them to IoT Hub in one call:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="ed067-230">您或許已經猜到，此程式碼的結果是兩個資料事件都會傳送到 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="ed067-230">You might guess that the result of this code is that two data events are sent to IoT Hub:</span></span>

<span data-ttu-id="ed067-231">[</span><span class="sxs-lookup"><span data-stu-id="ed067-231">[</span></span>

<span data-ttu-id="ed067-232">{"Temperature":75},</span><span class="sxs-lookup"><span data-stu-id="ed067-232">{"Temperature":75},</span></span>

<span data-ttu-id="ed067-233">{"Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="ed067-233">{"Humidity":45}</span></span>

<span data-ttu-id="ed067-234">]</span><span class="sxs-lookup"><span data-stu-id="ed067-234">]</span></span>

<span data-ttu-id="ed067-235">換句話說，您可以預期此程式碼與分別傳送 **Temperature** 和 **Humidity** 一樣。</span><span class="sxs-lookup"><span data-stu-id="ed067-235">In other words, you might expect that this code is the same as sending **Temperature** and **Humidity** separately.</span></span> <span data-ttu-id="ed067-236">這樣就可以方便將兩個事件在相同的呼叫中傳遞到 **SERIALIZE** 。</span><span class="sxs-lookup"><span data-stu-id="ed067-236">It’s just a convenience to pass both events to **SERIALIZE** in the same call.</span></span> <span data-ttu-id="ed067-237">不過，事實並非如此。</span><span class="sxs-lookup"><span data-stu-id="ed067-237">However, that’s not the case.</span></span> <span data-ttu-id="ed067-238">上述程式碼會改為將這個單一資料事件傳送到 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="ed067-238">Instead, the code above sends this single data event to IoT Hub:</span></span>

<span data-ttu-id="ed067-239">{"Temperature":75, "Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="ed067-239">{"Temperature":75, "Humidity":45}</span></span>

<span data-ttu-id="ed067-240">這可能看似奇怪，因為我們的模型將 **Temperature** 和 **Humidity** 定義成兩個「個別」事件：</span><span class="sxs-lookup"><span data-stu-id="ed067-240">This may seem strange because our model defines **Temperature** and **Humidity** as two *separate* events:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="ed067-241">此外，我們沒有將 **Temperature** 和 **Humidity** 位於相同結構中的這些事件模型化：</span><span class="sxs-lookup"><span data-stu-id="ed067-241">More to the point, we didn’t model these events where **Temperature** and **Humidity** are in the same structure:</span></span>

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

<span data-ttu-id="ed067-242">如果我們使用了這個模型，就會更容易了解如何在相同的序列化訊息中傳送 **Temperature** 和 **Humidity**。</span><span class="sxs-lookup"><span data-stu-id="ed067-242">If we used this model, it would be easier to understand how **Temperature** and **Humidity** would be sent in the same serialized message.</span></span> <span data-ttu-id="ed067-243">不過，如果您是使用模型 2 將兩個資料事件都傳遞至 **SERIALIZE** ，可能就無法突顯它以該方式運作的原因。</span><span class="sxs-lookup"><span data-stu-id="ed067-243">However it may not be clear why it works that way when you pass both data events to **SERIALIZE** using model 2.</span></span>

<span data-ttu-id="ed067-244">如果您知道 **序列化程式** 程式庫所做的假設，您可以更容易了解這種行為。</span><span class="sxs-lookup"><span data-stu-id="ed067-244">This behavior is easier to understand if you know the assumptions that the **serializer** library is making.</span></span> <span data-ttu-id="ed067-245">若要了解這一點，讓我們回到我們的模型：</span><span class="sxs-lookup"><span data-stu-id="ed067-245">To make sense of this let’s go back to our model:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="ed067-246">請以物件導向的觀點思考此模型。</span><span class="sxs-lookup"><span data-stu-id="ed067-246">Think of this model in object-oriented terms.</span></span> <span data-ttu-id="ed067-247">在此案例中，我們要模型化的是一個實體裝置 (控溫器)，而該裝置包含 **Temperature** 和 **Humidity** 之類的屬性。</span><span class="sxs-lookup"><span data-stu-id="ed067-247">In this case we’re modeling a physical device (a thermostat) and that device includes attributes like **Temperature** and **Humidity**.</span></span>

<span data-ttu-id="ed067-248">我們可以利用類似以下的程式碼來傳送模型的整個狀態：</span><span class="sxs-lookup"><span data-stu-id="ed067-248">We can send the entire state of our model with code such as the following:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="ed067-249">假設已設定溫度、溼度和時間的值，我們會看到這樣的事件傳送到 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="ed067-249">Assuming the values of Temperature, Humidity and Time are set, we would see an event like this sent to IoT Hub:</span></span>

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="ed067-250">有時，您可能只想將模型的「部分」  屬性傳送到雲端 (尤其是當您的模型包含大量資料事件的時候)。</span><span class="sxs-lookup"><span data-stu-id="ed067-250">Sometimes you may only want to send *some* properties of the model to the cloud (this is especially true if your model contains a large number of data events).</span></span> <span data-ttu-id="ed067-251">這時，只傳送資料事件的子集會相當有用，就像我們先前的範例一樣：</span><span class="sxs-lookup"><span data-stu-id="ed067-251">It’s useful to send only a subset of data events, such as in our earlier example:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="ed067-252">這會產生如同我們使用 **Temperature** 和 **Time** 成員來定義 **TemperatureEvent** 一樣的完全相同 (就像我們在模型 1 所做的一樣) 序列化事件。</span><span class="sxs-lookup"><span data-stu-id="ed067-252">This generates exactly the same serialized event as if we had defined a **TemperatureEvent** with a **Temperature** and **Time** member, just as we did with model 1.</span></span> <span data-ttu-id="ed067-253">在此案例中，我們已可以使用不同的模型 (模型 2) 來產生完全相同的序列化事件，因為我們是以不同的方式呼叫 **SERIALIZE** 。</span><span class="sxs-lookup"><span data-stu-id="ed067-253">In this case we were able to generate exactly the same serialized event by using a different model (model 2) because we called **SERIALIZE** in a different way.</span></span>

<span data-ttu-id="ed067-254">重點是，如果您將多個資料事件傳送給 **SERIALIZE** ，則它會假設每個事件都是單一 JSON 物件中的一個屬性。</span><span class="sxs-lookup"><span data-stu-id="ed067-254">The important point is that if you pass multiple data events to **SERIALIZE,** then it assumes each event is a property in a single JSON object.</span></span>

<span data-ttu-id="ed067-255">最佳方法取決於您及您對模型的思考方式。</span><span class="sxs-lookup"><span data-stu-id="ed067-255">The best approach depends on you and how you think about your model.</span></span> <span data-ttu-id="ed067-256">如果您要將「事件」傳送至雲端，且每個事件都包含一組已定義的屬性，則第一種方法較為適合。</span><span class="sxs-lookup"><span data-stu-id="ed067-256">If you’re sending "events" to the cloud and each event contains a defined set of properties, then the first approach makes a lot of sense.</span></span> <span data-ttu-id="ed067-257">在該情況下，您會使用 **DECLARE\_STRUCT** 來定義每個事件的結構，然後利用 **WITH\_DATA** 巨集將它們包含在模型中。</span><span class="sxs-lookup"><span data-stu-id="ed067-257">In that case you would use **DECLARE\_STRUCT** to define the structure of each event and then include them in your model with the **WITH\_DATA** macro.</span></span> <span data-ttu-id="ed067-258">然後您會依照我們在上述第一個範例中使用的方法來傳送每個事件。</span><span class="sxs-lookup"><span data-stu-id="ed067-258">Then you send each event as we did in the first example above.</span></span> <span data-ttu-id="ed067-259">採用此方法時，您只會傳送單一資料事件給 **SERIALIZER**。</span><span class="sxs-lookup"><span data-stu-id="ed067-259">In this approach you would only pass a single data event to **SERIALIZER**.</span></span>

<span data-ttu-id="ed067-260">如果您以物件導向的方式思考模型，則第二種方法可能比較適合您。</span><span class="sxs-lookup"><span data-stu-id="ed067-260">If you think about your model in an object-oriented fashion, then the second approach may suit you.</span></span> <span data-ttu-id="ed067-261">在此情況下，使用 **WITH\_DATA** 來定義的元素是您物件的「屬性」。</span><span class="sxs-lookup"><span data-stu-id="ed067-261">In this case, the elements defined using **WITH\_DATA** are the "properties" of your object.</span></span> <span data-ttu-id="ed067-262">您可以依據想要傳送至雲端的「物件」狀態詳細程度而定，隨意傳遞事件的任何子集給 **SERIALIZE** 。</span><span class="sxs-lookup"><span data-stu-id="ed067-262">You pass whatever subset of events to **SERIALIZE** that you like, depending on how much of your "object’s" state you want to send to the cloud.</span></span>

<span data-ttu-id="ed067-263">沒有絕對正確或錯誤的方法。</span><span class="sxs-lookup"><span data-stu-id="ed067-263">Nether approach is right or wrong.</span></span> <span data-ttu-id="ed067-264">請務必了解 **序列化程式** 程式庫的運作方式，並挑選最適合您需求的模型化方法。</span><span class="sxs-lookup"><span data-stu-id="ed067-264">Just be aware of how the **serializer** library works, and pick the modeling approach that best fits your needs.</span></span>

## <a name="message-handling"></a><span data-ttu-id="ed067-265">訊息處理</span><span class="sxs-lookup"><span data-stu-id="ed067-265">Message handling</span></span>
<span data-ttu-id="ed067-266">到目前為止，本文只討論傳送事件到 IoT 中樞，尚未處理接收訊息。</span><span class="sxs-lookup"><span data-stu-id="ed067-266">So far this article has only discussed sending events to IoT Hub, and hasn't addressed receiving messages.</span></span> <span data-ttu-id="ed067-267">這是因為有關接收訊息的相關內容在 [先前的文章](iot-hub-device-sdk-c-intro.md)中已涵蓋大部分資訊。</span><span class="sxs-lookup"><span data-stu-id="ed067-267">The reason for this is that what we need to know about receiving messages has largely been covered in an [earlier article](iot-hub-device-sdk-c-intro.md).</span></span> <span data-ttu-id="ed067-268">請從那篇文章回憶，您是藉由註冊訊息回呼函式來處理訊息：</span><span class="sxs-lookup"><span data-stu-id="ed067-268">Recall from that article that you process messages by registering a message callback function:</span></span>

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

<span data-ttu-id="ed067-269">然後撰寫在接收訊息時所叫用的回呼函式：</span><span class="sxs-lookup"><span data-stu-id="ed067-269">You then write the callback function that’s invoked when a message is received:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable to IoTHubMessage_GetByteArray\r\n");
        result = EXECUTE_COMMAND_ERROR;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed to malloc\r\n");
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

<span data-ttu-id="ed067-270">**IoTHubMessage** 的實作會針對您模型中的每個動作呼叫特定的函式。</span><span class="sxs-lookup"><span data-stu-id="ed067-270">This implementation of **IoTHubMessage** calls the specific function for each action in your model.</span></span> <span data-ttu-id="ed067-271">例如，如果您的模型定義這項動作：</span><span class="sxs-lookup"><span data-stu-id="ed067-271">For example, if your model defines this action:</span></span>

```
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="ed067-272">您必須使用此簽章定義函式：</span><span class="sxs-lookup"><span data-stu-id="ed067-272">You must define a function with this signature:</span></span>

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position to %d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="ed067-273">**SetAirResistance** 。</span><span class="sxs-lookup"><span data-stu-id="ed067-273">**SetAirResistance** is then called when that message is sent to your device.</span></span>

<span data-ttu-id="ed067-274">不過我們還沒說明序列化版本訊息的外觀。</span><span class="sxs-lookup"><span data-stu-id="ed067-274">What we haven't explained yet is what the serialized version of message looks like.</span></span> <span data-ttu-id="ed067-275">換句話說，如果您想要傳送 **SetAirResistance** 訊息至您的裝置，該訊息的外觀如何？</span><span class="sxs-lookup"><span data-stu-id="ed067-275">In other words, if you want to send a **SetAirResistance** message to your device, what does that look like?</span></span>

<span data-ttu-id="ed067-276">如果您要傳送訊息給裝置，您會透過 Azure IoT 服務 SDK 進行。</span><span class="sxs-lookup"><span data-stu-id="ed067-276">If you're sending a message to a device, you would do so through the Azure IoT service SDK.</span></span> <span data-ttu-id="ed067-277">您仍然需要知道要傳送哪個字串才能叫用特殊動作。</span><span class="sxs-lookup"><span data-stu-id="ed067-277">You still need to know what string to send to invoke a particular action.</span></span> <span data-ttu-id="ed067-278">傳送訊息的一般格式看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="ed067-278">The general format for sending a message appears as follows:</span></span>

```
{"Name" : "", "Parameters" : "" }
```

<span data-ttu-id="ed067-279">您將使用兩個屬性來傳送序列化的 JSON 物件：**Name** 是動作 (訊息) 的名稱，而 **Parameters** 則包含該動作的參數。</span><span class="sxs-lookup"><span data-stu-id="ed067-279">You're sending a serialized JSON object with two properties: **Name** is the name of the action (message) and **Parameters** contains the parameters of that action.</span></span>

<span data-ttu-id="ed067-280">例如，若要叫用 **SetAirResistance** ，您可以將下列訊息傳送給裝置：</span><span class="sxs-lookup"><span data-stu-id="ed067-280">For example, to invoke **SetAirResistance** you can send this message to a device:</span></span>

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

<span data-ttu-id="ed067-281">動作名稱必須完全符合您的模型中所定義的動作。</span><span class="sxs-lookup"><span data-stu-id="ed067-281">The action name must exactly match an action defined in your model.</span></span> <span data-ttu-id="ed067-282">參數名稱也必須相符。</span><span class="sxs-lookup"><span data-stu-id="ed067-282">The parameter names must match as well.</span></span> <span data-ttu-id="ed067-283">也請注意區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="ed067-283">Also note case sensitivity.</span></span> <span data-ttu-id="ed067-284">**Name** 和 **Parameters** 一律是大寫。</span><span class="sxs-lookup"><span data-stu-id="ed067-284">**Name** and **Parameters** are always uppercase.</span></span> <span data-ttu-id="ed067-285">請務必符合您模型中動作名稱和參數的大小寫。</span><span class="sxs-lookup"><span data-stu-id="ed067-285">Make sure to match the case of your action name and parameters in your model.</span></span> <span data-ttu-id="ed067-286">在此範例中，動作名稱是 "SetAirResistance"，而不是 "setairresistance"。</span><span class="sxs-lookup"><span data-stu-id="ed067-286">In this example, the action name is "SetAirResistance" and not "setairresistance".</span></span>

<span data-ttu-id="ed067-287">您可以透過將下列訊息傳送到裝置，以叫用兩個其他動作 **TurnFanOn** 與 **TurnFanOff**：</span><span class="sxs-lookup"><span data-stu-id="ed067-287">The two other actions **TurnFanOn** and **TurnFanOff** can be invoked by sending these messages to a device:</span></span>

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

<span data-ttu-id="ed067-288">本節說明使用 **序列化程式** 程式庫來傳送事件及接收訊息時的一切資訊。</span><span class="sxs-lookup"><span data-stu-id="ed067-288">This section described everything you need to know when sending events and receiving messages with the **serializer** library.</span></span> <span data-ttu-id="ed067-289">在繼續討論之前，讓我們先討論一些您可以設定以控制模型大小的參數。</span><span class="sxs-lookup"><span data-stu-id="ed067-289">Before moving on, let's cover some parameters you can configure that control how large your model is.</span></span>

## <a name="macro-configuration"></a><span data-ttu-id="ed067-290">巨集組態</span><span class="sxs-lookup"><span data-stu-id="ed067-290">Macro configuration</span></span>
<span data-ttu-id="ed067-291">如果您使用 **序列化程式** 程式庫，需注意的 SDK 重點位於 azure-c-shared-utility 程式庫中。</span><span class="sxs-lookup"><span data-stu-id="ed067-291">If you’re using the **Serializer** library an important part of the SDK to be aware of is found in the azure-c-shared-utility library.</span></span>
<span data-ttu-id="ed067-292">如果您已經利用 --recursive 選項，從 GitHub 複製 Azure-iot-sdk-c 儲存機制，您就可以在以下位置找到這個共用公用程式庫：</span><span class="sxs-lookup"><span data-stu-id="ed067-292">If you have cloned the Azure-iot-sdk-c repository from GitHub using the --recursive option, then you will find this shared utility library here:</span></span>

```
.\\c-utility
```

<span data-ttu-id="ed067-293">如果您尚未複製程式庫，可以在 [這裡](https://github.com/Azure/azure-c-shared-utility)找到。</span><span class="sxs-lookup"><span data-stu-id="ed067-293">If you have not cloned the library, you can find it [here](https://github.com/Azure/azure-c-shared-utility).</span></span>

<span data-ttu-id="ed067-294">在共用公用程式庫中，可以找到下列資料夾：</span><span class="sxs-lookup"><span data-stu-id="ed067-294">Within the shared utility library, you will find the following folder:</span></span>

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

<span data-ttu-id="ed067-295">此資料夾包含名為 **macro\_utils\_h\_generator.sln** 的 Visual Studio 方案：</span><span class="sxs-lookup"><span data-stu-id="ed067-295">This folder contains a Visual Studio solution called **macro\_utils\_h\_generator.sln**:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

<span data-ttu-id="ed067-296">此方案中的程式會產生 **macro\_utils.h** 檔案。</span><span class="sxs-lookup"><span data-stu-id="ed067-296">The program in this solution generates the **macro\_utils.h** file.</span></span> <span data-ttu-id="ed067-297">SDK 有一個隨附的預設 macro\_utils.h 檔案。</span><span class="sxs-lookup"><span data-stu-id="ed067-297">There’s a default macro\_utils.h file included with the SDK.</span></span> <span data-ttu-id="ed067-298">這個解決方案可讓您修改部分參數，然後根據這些參數重新建立標頭檔。</span><span class="sxs-lookup"><span data-stu-id="ed067-298">This solution allows you to modify some parameters and then recreate the header file based on these parameters.</span></span>

<span data-ttu-id="ed067-299">要考慮的兩個重要參數為 **nArithmetic** 和 **nMacroParameters**，這些參數是定義在 macro\_utils.tt 中的這兩行：</span><span class="sxs-lookup"><span data-stu-id="ed067-299">The two key parameters to be concerned with are **nArithmetic** and **nMacroParameters** which are defined in these two lines found in macro\_utils.tt:</span></span>

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

<span data-ttu-id="ed067-300">這些值是 SDK 隨附的預設參數。</span><span class="sxs-lookup"><span data-stu-id="ed067-300">These values are the default parameters included with the SDK.</span></span> <span data-ttu-id="ed067-301">每個參數都具有下列意義：</span><span class="sxs-lookup"><span data-stu-id="ed067-301">Each parameter has the following meaning:</span></span>

* <span data-ttu-id="ed067-302">nMacroParameters – 控制您在一個 DECLARE\_MODEL 巨集定義中可以擁有多少參數。</span><span class="sxs-lookup"><span data-stu-id="ed067-302">nMacroParameters – Controls how many parameters you can have in one DECLARE\_MODEL macro definition.</span></span>
* <span data-ttu-id="ed067-303">nArithmetic – 控制模型中允許的成員總數。</span><span class="sxs-lookup"><span data-stu-id="ed067-303">nArithmetic – Controls the total number of members allowed in a model.</span></span>

<span data-ttu-id="ed067-304">這些參數之所以重要，是因為它們控制您模型的大小。</span><span class="sxs-lookup"><span data-stu-id="ed067-304">The reason these parameters are important is because they control how large your model can be.</span></span> <span data-ttu-id="ed067-305">例如，請考慮以此模型定義：</span><span class="sxs-lookup"><span data-stu-id="ed067-305">For example, consider this model definition:</span></span>

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

<span data-ttu-id="ed067-306">如先前所述，**DECLARE\_MODEL** 只是一個 C 巨集。</span><span class="sxs-lookup"><span data-stu-id="ed067-306">As mentioned previously, **DECLARE\_MODEL** is just a C macro.</span></span> <span data-ttu-id="ed067-307">模型的名稱和 **WITH\_DATA** 陳述式 (另一個巨集) 是 **DECLARE\_MODEL** 的參數。</span><span class="sxs-lookup"><span data-stu-id="ed067-307">The names of the model and the **WITH\_DATA** statement (yet another macro) are parameters of **DECLARE\_MODEL**.</span></span> <span data-ttu-id="ed067-308">**nMacroParameters** 會定義 **DECLARE\_MODEL** 中可以包含多少參數。</span><span class="sxs-lookup"><span data-stu-id="ed067-308">**nMacroParameters** defines how many parameters can be included in **DECLARE\_MODEL**.</span></span> <span data-ttu-id="ed067-309">實際上，這定義的是您所能擁有的資料事件和動作宣告數目。</span><span class="sxs-lookup"><span data-stu-id="ed067-309">Effectively, this defines how many data event and action declarations you can have.</span></span> <span data-ttu-id="ed067-310">因此，使用預設限制 124 時，表示您可以定義由大約 60 個動作和事件資料所組成的模型。</span><span class="sxs-lookup"><span data-stu-id="ed067-310">As such, with the default limit of 124 this means that you can define a model with a combination of about 60 actions and data events.</span></span> <span data-ttu-id="ed067-311">如果您嘗試超過這個限制，您會收到看起來像這樣的編譯器錯誤：</span><span class="sxs-lookup"><span data-stu-id="ed067-311">If you try to exceed this limit, you'll receive compiler errors that look similar to this:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

<span data-ttu-id="ed067-312">**nArithmetic** 參數與巨集語言的內部運作較有關，與您的應用程式較無關。</span><span class="sxs-lookup"><span data-stu-id="ed067-312">The **nArithmetic** parameter is more about the internal workings of the macro language than your application.</span></span>  <span data-ttu-id="ed067-313">它會控制您可以在模型中擁有的成員總數，包括 **DECLARE_STRUCT** 巨集。</span><span class="sxs-lookup"><span data-stu-id="ed067-313">It controls the total number of members you can have in your model, including **DECLARE_STRUCT** macros.</span></span> <span data-ttu-id="ed067-314">如果您開始看到這類編譯器錯誤，則應該嘗試提高 **nArithmetic**的值：</span><span class="sxs-lookup"><span data-stu-id="ed067-314">If you start seeing compiler errors such as this, then you should try increasing **nArithmetic**:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

<span data-ttu-id="ed067-315">如果您想要變更這些參數，請修改 macro\_utils.tt 檔案中的值、重新編譯 macro\_utils\_h\_generator.sln 方案，然後執行編譯過的程式。</span><span class="sxs-lookup"><span data-stu-id="ed067-315">If you want to change these parameters, modify the values in the macro\_utils.tt file, recompile the macro\_utils\_h\_generator.sln solution, and run the compiled program.</span></span> <span data-ttu-id="ed067-316">當您這麼做時，會產生新的 macro\_utils.h 檔案並放在 .\\common\\inc 目錄中。</span><span class="sxs-lookup"><span data-stu-id="ed067-316">When you do so, a new macro\_utils.h file is generated and placed in the .\\common\\inc directory.</span></span>

<span data-ttu-id="ed067-317">若要使用新版的 macro\_utils.h，請從您的方案中移除「序列化程式」NuGet 套件，並在其位置中納入「序列化程式」Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="ed067-317">In order to use the new version of macro\_utils.h, remove the **serializer** NuGet package from your solution and in its place include the **serializer** Visual Studio project.</span></span> <span data-ttu-id="ed067-318">這可讓您的程式碼針對序列化程式程式庫的原始程式碼進行編譯。</span><span class="sxs-lookup"><span data-stu-id="ed067-318">This enables your code to compile against the source code of the serializer library.</span></span> <span data-ttu-id="ed067-319">這包括已更新的 macro\_utils.h。</span><span class="sxs-lookup"><span data-stu-id="ed067-319">This includes the updated macro\_utils.h.</span></span> <span data-ttu-id="ed067-320">如果您想要針對 **simplesample\_amqp** 執行這項操作，請從自方案中移除序列化程式程式庫的 NuGet 套件開始：</span><span class="sxs-lookup"><span data-stu-id="ed067-320">If you want to do this for **simplesample\_amqp**, start by removing the NuGet package for the serializer library from the solution:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

<span data-ttu-id="ed067-321">然後將此專案新增到您的 Visual Studio 解決方案：</span><span class="sxs-lookup"><span data-stu-id="ed067-321">Then add this project to your Visual Studio solution:</span></span>

> <span data-ttu-id="ed067-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span><span class="sxs-lookup"><span data-stu-id="ed067-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span></span>
> 
> 

<span data-ttu-id="ed067-323">完成時，解決方案應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="ed067-323">When you're done, your solution should look like this:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

<span data-ttu-id="ed067-324">現在，當您編譯您的方案時，已更新的 macro\_utils.h 就會包含在您的二進位檔中。</span><span class="sxs-lookup"><span data-stu-id="ed067-324">Now when you compile your solution, the updated macro\_utils.h is included in your binary.</span></span>

<span data-ttu-id="ed067-325">請注意，增加這些值到足夠高的數目可能會超出編譯器限制。</span><span class="sxs-lookup"><span data-stu-id="ed067-325">Note that increasing these values high enough can exceed compiler limits.</span></span> <span data-ttu-id="ed067-326">到這個階段， **nMacroParameters** 會是需要納入考量的主要參數。</span><span class="sxs-lookup"><span data-stu-id="ed067-326">To this point, the **nMacroParameters** is the main parameter with which to be concerned.</span></span> <span data-ttu-id="ed067-327">C99 規格指定巨集定義中允許最少 127 個參數。</span><span class="sxs-lookup"><span data-stu-id="ed067-327">The C99 spec specifies that a minimum of 127 parameters are allowed in a macro definition.</span></span> <span data-ttu-id="ed067-328">Microsoft 編譯器完全遵循此規格 (限制為 127)，因此您無法將 **nMacroParameters** 提高到超過預設值。</span><span class="sxs-lookup"><span data-stu-id="ed067-328">The Microsoft compiler follows the spec exactly (and has a limit of 127), so you won't be able to increase **nMacroParameters** beyond the default.</span></span> <span data-ttu-id="ed067-329">其他編譯器可能會允許您這麼做 (例如 GNU 編譯器支援更高的限制)。</span><span class="sxs-lookup"><span data-stu-id="ed067-329">Other compilers might allow you to do so (for example, the GNU compiler supports a higher limit).</span></span>

<span data-ttu-id="ed067-330">到目前為止，我們幾乎已經討論了如何使用 **序列化程式** 程式庫撰寫程式碼所必須知道的一切內容。</span><span class="sxs-lookup"><span data-stu-id="ed067-330">So far we've covered just about everything you need to know about how to write code with the **serializer** library.</span></span> <span data-ttu-id="ed067-331">在做出結論之前，讓我們先從先前的文章中回顧一些您可能想知道的主題。</span><span class="sxs-lookup"><span data-stu-id="ed067-331">Before concluding, let's revisit some topics from previous articles that you may be wondering about.</span></span>

## <a name="the-lower-level-apis"></a><span data-ttu-id="ed067-332">較低層級的 API</span><span class="sxs-lookup"><span data-stu-id="ed067-332">The lower-level APIs</span></span>
<span data-ttu-id="ed067-333">本文著重的範例應用程式是 **simplesample\_amqp**。</span><span class="sxs-lookup"><span data-stu-id="ed067-333">The sample application on which this article focused is **simplesample\_amqp**.</span></span> <span data-ttu-id="ed067-334">這個範例使用較高層級 (非 "LL") API 來傳送事件和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="ed067-334">This sample uses the higher-level (the non-"LL") APIs to send events and receive messages.</span></span> <span data-ttu-id="ed067-335">如果您使用這些 API，將會執行背景執行緒來處理事件傳送和訊息接收。</span><span class="sxs-lookup"><span data-stu-id="ed067-335">If you use these APIs, a background thread runs which takes care of both sending events and receiving messages.</span></span> <span data-ttu-id="ed067-336">不過，您可以使用較低層級 (LL) API 來消除這個背景執行緒，並明確掌控傳送事件或從雲端接收訊息的時機。</span><span class="sxs-lookup"><span data-stu-id="ed067-336">However, you can use the lower-level (LL) APIs to eliminate this background thread and take explicit control over when you send events or receive messages from the cloud.</span></span>

<span data-ttu-id="ed067-337">如 [前一篇文章](iot-hub-device-sdk-c-iothubclient.md)所述，有一組由較高層級 API 組成的函式：</span><span class="sxs-lookup"><span data-stu-id="ed067-337">As described in a [previous article](iot-hub-device-sdk-c-iothubclient.md), there is a set of functions that consists of the higher-level APIs:</span></span>

* <span data-ttu-id="ed067-338">IoTHubClient\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="ed067-338">IoTHubClient\_CreateFromConnectionString</span></span>
* <span data-ttu-id="ed067-339">IoTHubClient\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="ed067-339">IoTHubClient\_SendEventAsync</span></span>
* <span data-ttu-id="ed067-340">IoTHubClient\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="ed067-340">IoTHubClient\_SetMessageCallback</span></span>
* <span data-ttu-id="ed067-341">IoTHubClient\_Destroy</span><span class="sxs-lookup"><span data-stu-id="ed067-341">IoTHubClient\_Destroy</span></span>

<span data-ttu-id="ed067-342">**simplesample\_amqp** 中會示範這些 API。</span><span class="sxs-lookup"><span data-stu-id="ed067-342">These APIs are demonstrated in **simplesample\_amqp**.</span></span>

<span data-ttu-id="ed067-343">此外，也有一組類似的較低層級 API。</span><span class="sxs-lookup"><span data-stu-id="ed067-343">There is also an analogous set of lower-level APIs.</span></span>

* <span data-ttu-id="ed067-344">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="ed067-344">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="ed067-345">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="ed067-345">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="ed067-346">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="ed067-346">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="ed067-347">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="ed067-347">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="ed067-348">請注意，較低層級 API 的運作方式與先前文章中所述的完全相同。</span><span class="sxs-lookup"><span data-stu-id="ed067-348">Note that the lower-level APIs work exactly the same way as described in the previous articles.</span></span> <span data-ttu-id="ed067-349">如果您想要背景執行緒以處理事件傳送和訊息接收，您可以使用第一組 API。</span><span class="sxs-lookup"><span data-stu-id="ed067-349">You can use the first set of APIs if you want a background thread to handle sending events and receiving messages.</span></span> <span data-ttu-id="ed067-350">如果您想要掌握與 IoT 中樞之間傳送和接收資料時的明確控制權，您可以使用第二組 API。</span><span class="sxs-lookup"><span data-stu-id="ed067-350">You use the second set of APIs if you want explicit control over when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="ed067-351">任何一組 API 使用 **序列化程式** 程式庫的效果都相同。</span><span class="sxs-lookup"><span data-stu-id="ed067-351">Either set of APIs work equally well with the **serializer** library.</span></span>

<span data-ttu-id="ed067-352">如需有關如何將較低層級 API 與「序列化程式」程式庫搭配使用的範例，請參閱 **simplesample\_http** 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed067-352">For an example of how the lower-level APIs are used with the **serializer** library, see the **simplesample\_http** application.</span></span>

## <a name="additional-topics"></a><span data-ttu-id="ed067-353">其他主題</span><span class="sxs-lookup"><span data-stu-id="ed067-353">Additional topics</span></span>
<span data-ttu-id="ed067-354">幾個其他值得再次一提的主題包括屬性處理、使用替代裝置認證及組態選項。</span><span class="sxs-lookup"><span data-stu-id="ed067-354">A few other topics worth mentioning again are property handling, using alternate device credentials, and configuration options.</span></span> <span data-ttu-id="ed067-355">這些都是 [先前的文章](iot-hub-device-sdk-c-iothubclient.md)中所涵蓋的主題。</span><span class="sxs-lookup"><span data-stu-id="ed067-355">These are all topics covered in a [previous article](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="ed067-356">重點在於，所有這些功能不論是與「序列化程式」程式庫搭配，還是與 **IoTHubClient** 程式庫搭配，其運作方式均相同。</span><span class="sxs-lookup"><span data-stu-id="ed067-356">The main point is that all of these features work in the same way with the **serializer** library as they do with the **IoTHubClient** library.</span></span> <span data-ttu-id="ed067-357">例如，如果您想要將屬性附加到來自您模型的事件，您需透過前述的相同方式，使用 **IoTHubMessage\_Properties** 和 **Map**\_**AddorUpdate**：</span><span class="sxs-lookup"><span data-stu-id="ed067-357">For example, if you want to attach properties to an event from your model, you use **IoTHubMessage\_Properties** and **Map**\_**AddorUpdate**, the same way as described previously:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="ed067-358">無論事件是從「序列化程式」程式庫產生，還是使用 **IoTHubClient** 程式庫手動建立，並不重要。</span><span class="sxs-lookup"><span data-stu-id="ed067-358">Whether the event was generated from the **serializer** library or created manually using the **IoTHubClient** library does not matter.</span></span>

<span data-ttu-id="ed067-359">就替代裝置認證而言，使用 **IoTHubClient\_LL\_Create** 來配置 **IOTHUB\_CLIENT\_HANDLE** 的效果與使用 **IoTHubClient\_CreateFromConnectionString** 一樣好。</span><span class="sxs-lookup"><span data-stu-id="ed067-359">For the alternate device credentials, using **IoTHubClient\_LL\_Create** works just as well as **IoTHubClient\_CreateFromConnectionString** for allocating an **IOTHUB\_CLIENT\_HANDLE**.</span></span>

<span data-ttu-id="ed067-360">最後，如果您使用「序列化程式」程式庫，就可以使用 **IoTHubClient\_LL\_SetOption** 來設定組態選項，就像您使用 **IoTHubClient** 程式庫時所做的一樣。</span><span class="sxs-lookup"><span data-stu-id="ed067-360">Finally, if you're using the **serializer** library, you can set configuration options with **IoTHubClient\_LL\_SetOption** just as you did when using the **IoTHubClient** library.</span></span>

<span data-ttu-id="ed067-361">**序列化程式** 程式庫有一個獨一無二的功能，也就是初始化 API。</span><span class="sxs-lookup"><span data-stu-id="ed067-361">A feature that is unique to the **serializer** library are the initialization APIs.</span></span> <span data-ttu-id="ed067-362">您必須先呼叫 **serializer\_init**，才能開始使用該程式庫：</span><span class="sxs-lookup"><span data-stu-id="ed067-362">Before you can start working with the library, you must call **serializer\_init**:</span></span>

```
serializer_init(NULL);
```

<span data-ttu-id="ed067-363">此動作必須正好在呼叫 **IoTHubClient\_CreateFromConnectionString** 之前執行。</span><span class="sxs-lookup"><span data-stu-id="ed067-363">This is done just before you call **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="ed067-364">同樣地，當您使用完該程式庫時，最後呼叫的對象會是 **serializer\_deinit**：</span><span class="sxs-lookup"><span data-stu-id="ed067-364">Similarly, when you're done working with the library, the last call you’ll make is to **serializer\_deinit**:</span></span>

```
serializer_deinit();
```

<span data-ttu-id="ed067-365">除此之外，上面列出的所有其他功能在「序列化程式」程式庫中的運作方式，皆與在 **IoTHubClient** 程式庫中的運作方式相同。</span><span class="sxs-lookup"><span data-stu-id="ed067-365">Otherwise, all of the other features listed above work the same in the **serializer** library as they do in the **IoTHubClient** library.</span></span> <span data-ttu-id="ed067-366">如需有關任何這些主題的詳細資訊，請參閱本系列中的 [前一篇文章](iot-hub-device-sdk-c-iothubclient.md) 。</span><span class="sxs-lookup"><span data-stu-id="ed067-366">For more information about any of these topics, see the [previous article](iot-hub-device-sdk-c-iothubclient.md) in this series.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed067-367">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ed067-367">Next steps</span></span>
<span data-ttu-id="ed067-368">本文詳細說明「適用於 C 的 Azure IoT 裝置 SDK」中所含「序列化程式」程式庫的獨特層面。透過文中提供的資訊，您應該能充分了解如何使用模型來傳送事件和接收來自 IoT 中樞的訊息。</span><span class="sxs-lookup"><span data-stu-id="ed067-368">This article describes in detail the unique aspects of the **serializer** library contained in the **Azure IoT device SDK for C**. With the information provided you should have a good understanding of how to use models to send events and receive messages from IoT Hub.</span></span>

<span data-ttu-id="ed067-369">這也結束了有關如何使用「適用於 C 的 Azure IoT 裝置 SDK」來開發應用程式的三部曲系列。這些資訊應該不僅足以讓您入門，還能讓您徹底了解 API 的運作方式。</span><span class="sxs-lookup"><span data-stu-id="ed067-369">This also concludes the three-part series on how to develop applications with the **Azure IoT device SDK for C**. This should be enough information to not only get you started but give you a thorough understanding of how the APIs work.</span></span> <span data-ttu-id="ed067-370">如需其他資訊，還有一些 SDK 中的範例未涵蓋在本文中。</span><span class="sxs-lookup"><span data-stu-id="ed067-370">For additional information, there are a few samples in the SDK not covered here.</span></span> <span data-ttu-id="ed067-371">除此之外， [SDK 文件](https://github.com/Azure/azure-iot-sdk-c) 也是取得其他資訊的絕佳資源。</span><span class="sxs-lookup"><span data-stu-id="ed067-371">Otherwise, the [SDK documentation](https://github.com/Azure/azure-iot-sdk-c) is a good resource for additional information.</span></span>

<span data-ttu-id="ed067-372">若要深入了解如何開發 IoT 中樞，請參閱 [Azure IoT SDK][lnk-sdks]。</span><span class="sxs-lookup"><span data-stu-id="ed067-372">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="ed067-373">若要進一步探索 IoT 中樞的功能，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="ed067-373">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="ed067-374">[使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="ed067-374">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
