---
title: "aaaUnderstand Azure IoT Hub 裝置雙 |Microsoft 文件"
description: "開發人員指南-使用裝置雙 toosynchronize IoT 中樞與您的裝置之間的狀態和組態資料"
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 8a3da072-a5bf-46e5-8de4-24cdbb2a03fa
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7dade18665108ed352ff3d18e864dc34f451bbf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a><span data-ttu-id="2a0b8-103">了解和使用 Azure IoT 中樞的裝置對應項</span><span class="sxs-lookup"><span data-stu-id="2a0b8-103">Understand and use device twins in IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="2a0b8-104">概觀</span><span class="sxs-lookup"><span data-stu-id="2a0b8-104">Overview</span></span>
<span data-ttu-id="2a0b8-105">「裝置對應項」是存放裝置狀態資訊 (中繼資料、組態和條件) 的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-105">*Device twins* are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="2a0b8-106">IoT 中樞保存您連接 tooIoT 中樞的每個裝置的裝置兩個。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-106">IoT Hub persists a device twin for each device that you connect tooIoT Hub.</span></span> <span data-ttu-id="2a0b8-107">本文章說明：</span><span class="sxs-lookup"><span data-stu-id="2a0b8-107">This article describes:</span></span>

* <span data-ttu-id="2a0b8-108">hello 的 hello 裝置兩個結構：*標記*，*所需*和*報告屬性*，和</span><span class="sxs-lookup"><span data-stu-id="2a0b8-108">hello structure of hello device twin: *tags*, *desired* and *reported properties*, and</span></span>
* <span data-ttu-id="2a0b8-109">hello 裝置應用程式和後端可以雙裝置執行的作業。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-109">hello operations that device apps and back ends can perform on device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="2a0b8-110">目前，只連線 tooIoT 中樞的裝置可以存取裝置雙會使用 hello MQTT 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-110">Currently, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="2a0b8-111">請參閱 toohello [MQTT 支援][ lnk-devguide-mqtt]文章的指示現有裝置的應用程式 toouse tooconvert MQTT。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-111">Refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>
> 
> 

### <a name="when-toouse"></a><span data-ttu-id="2a0b8-112">當 toouse</span><span class="sxs-lookup"><span data-stu-id="2a0b8-112">When toouse</span></span>
<span data-ttu-id="2a0b8-113">使用裝置對應項可以：</span><span class="sxs-lookup"><span data-stu-id="2a0b8-113">Use device twins to:</span></span>

* <span data-ttu-id="2a0b8-114">Hello 雲端中儲存裝置專屬的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-114">Store device-specific metadata in hello cloud.</span></span> <span data-ttu-id="2a0b8-115">例如，hello 販賣的部署位置。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-115">For example, hello deployment location of a vending machine.</span></span>
* <span data-ttu-id="2a0b8-116">從您的裝置應用程式報告目前狀態資訊，例如可用功能和狀況。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-116">Report current state information such as available capabilities and conditions from your device app.</span></span> <span data-ttu-id="2a0b8-117">例如，裝置是已連線的 tooyour IoT 中樞 over 行動電話通訊或 Wi-fi。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-117">For example, a device is connected tooyour IoT hub over cellular or WiFi.</span></span>
* <span data-ttu-id="2a0b8-118">同步處理裝置應用程式與後端應用程式之間的長時間執行工作流程的 hello 的狀態。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-118">Synchronize hello state of long-running workflows between device app and back-end app.</span></span> <span data-ttu-id="2a0b8-119">比方說，當 hello 方案回結束指定 hello 新的韌體版本 tooinstall，和 hello 裝置應用程式報表 hello hello 更新程序的各個階段。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-119">For example, when hello solution back end specifies hello new firmware version tooinstall, and hello device app reports hello various stages of hello update process.</span></span>
* <span data-ttu-id="2a0b8-120">查詢裝置中繼資料、組態或狀態。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-120">Query your device metadata, configuration, or state.</span></span>

<span data-ttu-id="2a0b8-121">請參閱太[裝置到雲端通訊指引][ lnk-d2c-guidance]如需使用報告的內容、 裝置到雲端訊息或檔案上傳的指引。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-121">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] for guidance on using reported properties, device-to-cloud messages, or file upload.</span></span>
<span data-ttu-id="2a0b8-122">參照太[雲端到裝置通訊指引][ lnk-c2d-guidance]如需使用所需的屬性、 直接的方法或雲端到裝置訊息的指引。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-122">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] for guidance on using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="device-twins"></a><span data-ttu-id="2a0b8-123">裝置對應項</span><span class="sxs-lookup"><span data-stu-id="2a0b8-123">Device twins</span></span>
<span data-ttu-id="2a0b8-124">裝置對應項會儲存裝置相關資訊，以供︰</span><span class="sxs-lookup"><span data-stu-id="2a0b8-124">Device twins store device-related information that:</span></span>

* <span data-ttu-id="2a0b8-125">Toosynchronize 裝置條件和設定，可以使用裝置和後端。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-125">Device and back ends can use toosynchronize device conditions and configuration.</span></span>
* <span data-ttu-id="2a0b8-126">hello 方案後端可以使用 tooquery，與目標長時間執行的作業。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-126">hello solution back end can use tooquery and target long-running operations.</span></span>

<span data-ttu-id="2a0b8-127">已連結裝置的兩個 hello 生命週期 toohello 對應[裝置身分識別][lnk-identity]。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-127">hello lifecycle of a device twin is linked toohello corresponding [device identity][lnk-identity].</span></span> <span data-ttu-id="2a0b8-128">在 IoT 中樞建立或刪除新的裝置身分識別時，會隱含地建立和刪除裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-128">Device twins are implicitly created and deleted when a new device identity is created or deleted in IoT Hub.</span></span>

<span data-ttu-id="2a0b8-129">裝置的兩個是 JSON 文件，其中含有︰</span><span class="sxs-lookup"><span data-stu-id="2a0b8-129">A device twin is a JSON document that includes:</span></span>

* <span data-ttu-id="2a0b8-130">**標籤**。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-130">**Tags**.</span></span> <span data-ttu-id="2a0b8-131">一段 hello 方案後端的 hello JSON 文件可以讀取和寫入。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-131">A section of hello JSON document that hello solution back end can read from and write to.</span></span> <span data-ttu-id="2a0b8-132">標記不可見的 toodevice 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-132">Tags are not visible toodevice apps.</span></span>
* <span data-ttu-id="2a0b8-133">**所需屬性**。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-133">**Desired properties**.</span></span> <span data-ttu-id="2a0b8-134">使用此選項，以及報告的屬性 toosynchronize 裝置組態或條件。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-134">Used along with reported properties toosynchronize device configuration or conditions.</span></span> <span data-ttu-id="2a0b8-135">所需的屬性只能設定回 hello 解決方案結束和 hello 裝置應用程式可以讀取。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-135">Desired properties can only be set by hello solution back end and can be read by hello device app.</span></span> <span data-ttu-id="2a0b8-136">hello 裝置應用程式也會即時 hello 預期屬性中的變更通知。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-136">hello device app can also be notified in real time of changes in hello desired properties.</span></span>
* <span data-ttu-id="2a0b8-137">**報告屬性**。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-137">**Reported properties**.</span></span> <span data-ttu-id="2a0b8-138">搭配使用所需的屬性 toosynchronize 裝置組態或條件。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-138">Used along with desired properties toosynchronize device configuration or conditions.</span></span> <span data-ttu-id="2a0b8-139">報告的屬性只能 hello 裝置應用程式設定與能夠讀取和查詢 hello 方案後端。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-139">Reported properties can only be set by hello device app and can be read and queried by hello solution back end.</span></span>

<span data-ttu-id="2a0b8-140">此外，hello 裝置兩個 JSON 文件的 hello 根包含儲存在 hello hello 對應裝置身分識別的 hello 唯讀屬性[身分識別登錄][lnk-identity]。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-140">Additionally, hello root of hello device twin JSON document contains hello read-only properties from hello corresponding device identity stored in hello [identity registry][lnk-identity].</span></span>

![][img-twin]

<span data-ttu-id="2a0b8-141">下列範例中的 hello 顯示裝置的兩個 JSON 文件：</span><span class="sxs-lookup"><span data-stu-id="2a0b8-141">hello following example shows a device twin JSON document:</span></span>

        {
            "deviceId": "devA",
            "generationId": "123",
            "status": "enabled",
            "statusReason": "provisioned",
            "connectionState": "connected",
            "connectionStateUpdatedTime": "2015-02-28T16:24:48.789Z",
            "lastActivityTime": "2015-02-30T16:24:48.789Z",

            "tags": {
                "$etag": "123",
                "deploymentLocation": {
                    "building": "43",
                    "floor": "1"
                }
            },
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata" : {...},
                    "$version": 1
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": 55,
                    "$metadata" : {...},
                    "$version": 4
                }
            }
        }

<span data-ttu-id="2a0b8-142">在 hello 根物件是 hello 系統屬性，並且容器物件`tags`，兩者均`reported`和`desired`屬性。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-142">In hello root object, are hello system properties, and container objects for `tags` and both `reported` and `desired` properties.</span></span> <span data-ttu-id="2a0b8-143">hello`properties`容器包含某些唯讀項目 (`$metadata`， `$etag`，和`$version`) 所述 hello[裝置兩個中繼資料][ lnk-twin-metadata]和[開放式並行存取][ lnk-concurrency]區段。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-143">hello `properties` container contains some read-only elements (`$metadata`, `$etag`, and `$version`) described in hello [Device twin metadata][lnk-twin-metadata] and [Optimistic concurrency][lnk-concurrency] sections.</span></span>

### <a name="reported-property-example"></a><span data-ttu-id="2a0b8-144">報告屬性範例</span><span class="sxs-lookup"><span data-stu-id="2a0b8-144">Reported property example</span></span>
<span data-ttu-id="2a0b8-145">在 hello 上述範例中，包含 hello 裝置兩個`batteryLevel`hello 裝置應用程式所報告的屬性。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-145">In hello previous example, hello device twin contains a `batteryLevel` property that is reported by hello device app.</span></span> <span data-ttu-id="2a0b8-146">這個屬性可以可能 tooquery，並且根據上次報告的電池電量 hello 在裝置上運作。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-146">This property makes it possible tooquery and operate on devices based on hello last reported battery level.</span></span> <span data-ttu-id="2a0b8-147">其他範例包括 hello 裝置應用程式報告裝置功能或連接選項。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-147">Other examples include hello device app reporting device capabilities or connectivity options.</span></span>

> [!NOTE]
> <span data-ttu-id="2a0b8-148">報告的內容會簡化其中 hello 方案後端有興趣 hello 最後已知的屬性值的案例。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-148">Reported properties simplify scenarios where hello solution back end is interested in hello last known value of a property.</span></span> <span data-ttu-id="2a0b8-149">使用[裝置到雲端訊息][ lnk-d2c] hello 方案後端是否需要 tooprocess 裝置遙測 hello 格式，加上事件，例如時間序列的序列。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-149">Use [device-to-cloud messages][lnk-d2c] if hello solution back end needs tooprocess device telemetry in hello form of sequences of timestamped events, such as time series.</span></span>

### <a name="desired-property-example"></a><span data-ttu-id="2a0b8-150">所需屬性範例</span><span class="sxs-lookup"><span data-stu-id="2a0b8-150">Desired property example</span></span>
<span data-ttu-id="2a0b8-151">Hello 上述範例中，在 hello`telemetryConfig`裝置兩個想要與報告的內容可供 hello 方案後端與 hello 裝置應用程式 toosynchronize hello 遙測設定此裝置。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-151">In hello previous example, hello `telemetryConfig` device twin desired and reported properties are used by hello solution back end and hello device app toosynchronize hello telemetry configuration for this device.</span></span> <span data-ttu-id="2a0b8-152">例如：</span><span class="sxs-lookup"><span data-stu-id="2a0b8-152">For example:</span></span>

1. <span data-ttu-id="2a0b8-153">hello 方案後端設定預期的 hello 屬性與預期的 hello 組態值。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-153">hello solution back end sets hello desired property with hello desired configuration value.</span></span> <span data-ttu-id="2a0b8-154">以下是 hello hello 文件所需的 hello 屬性設定的一部分：</span><span class="sxs-lookup"><span data-stu-id="2a0b8-154">Here is hello portion of hello document with hello desired property set:</span></span>
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. <span data-ttu-id="2a0b8-155">hello 裝置應用程式會收到 hello 變更立即如果連線，或在 hello 先重新連線的通知。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-155">hello device app is notified of hello change immediately if connected, or at hello first reconnect.</span></span> <span data-ttu-id="2a0b8-156">hello 裝置應用程式接著會報告 hello 更新組態 (或使用 hello 的錯誤狀況`status`屬性)。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-156">hello device app then reports hello updated configuration (or an error condition using hello `status` property).</span></span> <span data-ttu-id="2a0b8-157">以下是 hello hello 部分報告屬性：</span><span class="sxs-lookup"><span data-stu-id="2a0b8-157">Here is hello portion of hello reported properties:</span></span>
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. <span data-ttu-id="2a0b8-158">hello 方案後端可以追蹤 hello 作業結果的 hello 組態跨許多裝置，藉由[查詢][ lnk-query]裝置雙。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-158">hello solution back end can track hello results of hello configuration operation across many devices, by [querying][lnk-query] device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="2a0b8-159">hello 上述程式碼片段的例子，最佳化來提高可讀性，其中一種方式 tooencode 的裝置組態和它的狀態。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-159">hello preceding snippets are examples, optimized for readability, of one way tooencode a device configuration and its status.</span></span> <span data-ttu-id="2a0b8-160">IoT 中樞並無特定的結構描述，如 hello 裝置兩個想要與報告 hello 裝置雙中的屬性。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-160">IoT Hub does not impose a specific schema for hello device twin desired and reported properties in hello device twins.</span></span>
> 
> 

<span data-ttu-id="2a0b8-161">您可以使用雙 toosynchronize 長時間執行作業，例如韌體更新。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-161">You can use twins toosynchronize long-running operations such as firmware updates.</span></span> <span data-ttu-id="2a0b8-162">如需有關如何 toouse 屬性 toosynchronize 及追蹤長時間執行的作業，跨裝置，請參閱[使用想要的話屬性 tooconfigure 裝置][lnk-twin-properties]。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-162">For more information on how toouse properties toosynchronize and track a long running operation across devices, see [Use desired properties tooconfigure devices][lnk-twin-properties].</span></span>

## <a name="back-end-operations"></a><span data-ttu-id="2a0b8-163">後端作業</span><span class="sxs-lookup"><span data-stu-id="2a0b8-163">Back-end operations</span></span>
<span data-ttu-id="2a0b8-164">使用下列不可部分完成的作業，透過 HTTP 公開 hello hello 裝置兩個操作 hello 方案後端：</span><span class="sxs-lookup"><span data-stu-id="2a0b8-164">hello solution back end operates on hello device twin using hello following atomic operations, exposed through HTTP:</span></span>

1. <span data-ttu-id="2a0b8-165">**依識別碼擷取裝置對應項**。此操作會傳回報告 hello 裝置兩個文件，包括標記，且想要，和系統屬性。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-165">**Retrieve device twin by id**. This operation returns hello device twin document, including tags and desired, reported, and system properties.</span></span>
2. <span data-ttu-id="2a0b8-166">**部份更新裝置對應項**。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-166">**Partially update device twin**.</span></span> <span data-ttu-id="2a0b8-167">Hello 方案後端 toopartially 更新 hello 標記或中裝置的兩個所需的屬性，可讓這項作業。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-167">This operation enables hello solution back end toopartially update hello tags or desired properties in a device twin.</span></span> <span data-ttu-id="2a0b8-168">加入或更新任何屬性的 JSON 文件以 hello 部分更新。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-168">hello partial update is expressed as a JSON document that adds or updates any property.</span></span> <span data-ttu-id="2a0b8-169">屬性設定太`null`會移除。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-169">Properties set too`null` are removed.</span></span> <span data-ttu-id="2a0b8-170">hello 下列範例會建立新的所需的屬性值與`{"newProperty": "newValue"}`，會覆寫的 hello 現有值`existingProperty`與`"otherNewValue"`，並移除`otherOldProperty`。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-170">hello following example creates a new desired property with value `{"newProperty": "newValue"}`, overwrites hello existing value of `existingProperty` with `"otherNewValue"`, and removes `otherOldProperty`.</span></span> <span data-ttu-id="2a0b8-171">預期的 tooexisting 屬性或標記，則會不進行任何其他變更：</span><span class="sxs-lookup"><span data-stu-id="2a0b8-171">No other changes are made tooexisting desired properties or tags:</span></span>
   
        {
            "properties": {
                "desired": {
                    "newProperty": {
                        "nestedProperty": "newValue"
                    },
                    "existingProperty": "otherNewValue",
                    "otherOldProperty": null
                }
            }
        }
3. <span data-ttu-id="2a0b8-172">**取代所需屬性**。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-172">**Replace desired properties**.</span></span> <span data-ttu-id="2a0b8-173">此作業可讓 hello 方案後端 toocompletely 覆寫所有現有的所需的內容，並以取代為新的 JSON 文件`properties/desired`。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-173">This operation enables hello solution back end toocompletely overwrite all existing desired properties and substitute a new JSON document for `properties/desired`.</span></span>
4. <span data-ttu-id="2a0b8-174">**取代標籤**。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-174">**Replace tags**.</span></span> <span data-ttu-id="2a0b8-175">此作業可讓 hello 方案後端 toocompletely 覆寫所有現有的標記，並以取代為新的 JSON 文件`tags`。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-175">This operation enables hello solution back end toocompletely overwrite all existing tags and substitute a new JSON document for `tags`.</span></span>
5. <span data-ttu-id="2a0b8-176">**接收對應項通知**。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-176">**Receive twin notifications**.</span></span> <span data-ttu-id="2a0b8-177">這項作業允許 hello 方案後端 toobe hello 兩個已修改時收到通知。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-177">This operation allows hello solution back end toobe notified when hello twin is modified.</span></span> <span data-ttu-id="2a0b8-178">toodo 因此，您的 IoT 解決方案需要 toocreate 路由和 tooset hello 資料來源等太*twinChangeEvents*。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-178">toodo so, your IoT solution needs toocreate a route and tooset hello Data Source equal too*twinChangeEvents*.</span></span> <span data-ttu-id="2a0b8-179">根據預設，不會傳送任何對應項通知，亦即預先不存在這類路由。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-179">By default, no twin notifications are sent, that is, no such routes pre-exist.</span></span> <span data-ttu-id="2a0b8-180">如果 hello 變動率過高，或其他原因，例如內部失敗，可能會將只有一個包含所有變更的通知傳送 hello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-180">If hello rate of change is too high, or for other reasons, such as internal failures, hello IoT Hub might send only one notification that contains all changes.</span></span> <span data-ttu-id="2a0b8-181">因此，如果您的應用程式需要可靠地稽核和記錄所有中間狀態，則仍建議您使用 D2C 訊息。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-181">So, if your application needs reliable auditing and logging of all intermediate states, then it is still recommended that you use D2C messages.</span></span> <span data-ttu-id="2a0b8-182">hello 兩個通知訊息包含屬性和內文。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-182">hello twin notification message includes properties, and body.</span></span>

    - <span data-ttu-id="2a0b8-183">屬性</span><span class="sxs-lookup"><span data-stu-id="2a0b8-183">Properties</span></span>

    | <span data-ttu-id="2a0b8-184">名稱</span><span class="sxs-lookup"><span data-stu-id="2a0b8-184">Name</span></span> | <span data-ttu-id="2a0b8-185">值</span><span class="sxs-lookup"><span data-stu-id="2a0b8-185">Value</span></span> |
    | --- | --- |
    <span data-ttu-id="2a0b8-186">$content-type</span><span class="sxs-lookup"><span data-stu-id="2a0b8-186">$content-type</span></span> | <span data-ttu-id="2a0b8-187">application/json</span><span class="sxs-lookup"><span data-stu-id="2a0b8-187">application/json</span></span> |
    <span data-ttu-id="2a0b8-188">$iothub-enqueuedtime</span><span class="sxs-lookup"><span data-stu-id="2a0b8-188">$iothub-enqueuedtime</span></span> |  <span data-ttu-id="2a0b8-189">傳送嗨通知時間</span><span class="sxs-lookup"><span data-stu-id="2a0b8-189">Time when hello notification was sent</span></span> |
    <span data-ttu-id="2a0b8-190">$iothub-message-source</span><span class="sxs-lookup"><span data-stu-id="2a0b8-190">$iothub-message-source</span></span> | <span data-ttu-id="2a0b8-191">twinChangeEvents</span><span class="sxs-lookup"><span data-stu-id="2a0b8-191">twinChangeEvents</span></span> |
    <span data-ttu-id="2a0b8-192">$content-encoding</span><span class="sxs-lookup"><span data-stu-id="2a0b8-192">$content-encoding</span></span> | <span data-ttu-id="2a0b8-193">utf-8</span><span class="sxs-lookup"><span data-stu-id="2a0b8-193">utf-8</span></span> |
    <span data-ttu-id="2a0b8-194">deviceId</span><span class="sxs-lookup"><span data-stu-id="2a0b8-194">deviceId</span></span> | <span data-ttu-id="2a0b8-195">Hello 裝置識別碼</span><span class="sxs-lookup"><span data-stu-id="2a0b8-195">Id of hello device</span></span> |
    <span data-ttu-id="2a0b8-196">hubName</span><span class="sxs-lookup"><span data-stu-id="2a0b8-196">hubName</span></span> | <span data-ttu-id="2a0b8-197">IoT 中樞名稱</span><span class="sxs-lookup"><span data-stu-id="2a0b8-197">Name of IoT Hub</span></span> |
    <span data-ttu-id="2a0b8-198">operationTimestamp</span><span class="sxs-lookup"><span data-stu-id="2a0b8-198">operationTimestamp</span></span> | <span data-ttu-id="2a0b8-199">作業的 [ISO8601] 時間戳記</span><span class="sxs-lookup"><span data-stu-id="2a0b8-199">[ISO8601] timestamp of operation</span></span> |
    <span data-ttu-id="2a0b8-200">iothub-message-schema</span><span class="sxs-lookup"><span data-stu-id="2a0b8-200">iothub-message-schema</span></span> | <span data-ttu-id="2a0b8-201">deviceLifecycleNotification</span><span class="sxs-lookup"><span data-stu-id="2a0b8-201">deviceLifecycleNotification</span></span> |
    <span data-ttu-id="2a0b8-202">opType</span><span class="sxs-lookup"><span data-stu-id="2a0b8-202">opType</span></span> | <span data-ttu-id="2a0b8-203">"replaceTwin" 或 "updateTwin"</span><span class="sxs-lookup"><span data-stu-id="2a0b8-203">"replaceTwin" or "updateTwin"</span></span> |

    <span data-ttu-id="2a0b8-204">訊息系統屬性會加上 hello`'$'`符號。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-204">Message system properties are prefixed with hello `'$'` symbol.</span></span>

    - <span data-ttu-id="2a0b8-205">內文</span><span class="sxs-lookup"><span data-stu-id="2a0b8-205">Body</span></span>
        
    <span data-ttu-id="2a0b8-206">本節包含所有 hello 兩個變更，以 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-206">This section includes all hello twin changes in a JSON format.</span></span> <span data-ttu-id="2a0b8-207">它是修補程式使用相同格式的 hello、 hello 的差異，就可以包含所有的兩個區段： 標記、 properties.reported、 properties.desired，和它包含 hello"$metadata"項目。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-207">It uses hello same format as a patch, with hello difference that it can contain all twin sections: tags, properties.reported, properties.desired, and that it contains hello “$metadata” elements.</span></span> <span data-ttu-id="2a0b8-208">例如，</span><span class="sxs-lookup"><span data-stu-id="2a0b8-208">For example,</span></span>
    ```
    {
        "properties": {
            "desired": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            },
            "reported": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            }
        }
    }
    ``` 

<span data-ttu-id="2a0b8-209">所有 hello 上述作業支援[開放式並行存取][ lnk-concurrency] ，而且需要 hello **ServiceConnect**權限，如同 hello[安全性] [ lnk-security]發行項。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-209">All hello preceding operations support [Optimistic concurrency][lnk-concurrency] and require hello **ServiceConnect** permission, as defined in hello [Security][lnk-security] article.</span></span>

<span data-ttu-id="2a0b8-210">此外 toothese 作業，hello 方案後端可以：</span><span class="sxs-lookup"><span data-stu-id="2a0b8-210">In addition toothese operations, hello solution back end can:</span></span>

* <span data-ttu-id="2a0b8-211">查詢使用 hello hello 裝置雙類似 SQL 的[IoT 中樞的查詢語言][lnk-query]。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-211">Query hello device twins using hello SQL-like [IoT Hub query language][lnk-query].</span></span>
* <span data-ttu-id="2a0b8-212">使用[作業][lnk-jobs]在大型裝置對應項集合上執行作業。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-212">Perform operations on large sets of device twins using [jobs][lnk-jobs].</span></span>

## <a name="device-operations"></a><span data-ttu-id="2a0b8-213">裝置作業</span><span class="sxs-lookup"><span data-stu-id="2a0b8-213">Device operations</span></span>
<span data-ttu-id="2a0b8-214">hello 裝置應用程式對 hello 裝置兩個使用 hello 下列不可部分完成的作業：</span><span class="sxs-lookup"><span data-stu-id="2a0b8-214">hello device app operates on hello device twin using hello following atomic operations:</span></span>

1. <span data-ttu-id="2a0b8-215">**擷取裝置對應項**。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-215">**Retrieve device twin**.</span></span> <span data-ttu-id="2a0b8-216">此操作會傳回 hello 裝置兩個文件 (包含標記和預期、 報告和系統屬性) 的 hello 目前連接的裝置。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-216">This operation returns hello device twin document (including tags and desired, reported and system properties) for hello currently connected device.</span></span>
2. <span data-ttu-id="2a0b8-217">**部分更新的報告屬性**。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-217">**Partially update reported properties**.</span></span> <span data-ttu-id="2a0b8-218">此作業可讓 hello 部分更新的 hello 報告 hello 目前連接裝置的屬性。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-218">This operation enables hello partial update of hello reported properties of hello currently connected device.</span></span> <span data-ttu-id="2a0b8-219">此作業會使用 hello 更新相同的 JSON 格式，它 hello 方案後端使用的部分更新的所需的屬性。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-219">This operation uses hello same JSON update format that hello solution back end uses for a partial update of desired properties.</span></span>
3. <span data-ttu-id="2a0b8-220">**觀察所需屬性**。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-220">**Observe desired properties**.</span></span> <span data-ttu-id="2a0b8-221">hello 目前連接的裝置可以選擇 toobe 所發生的任何更新需要 toohello 內容的通知。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-221">hello currently connected device can choose toobe notified of updates toohello desired properties when they happen.</span></span> <span data-ttu-id="2a0b8-222">hello 裝置收到的 hello hello 方案後端所執行的相同形式的更新 （部分或完整取代）。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-222">hello device receives hello same form of update (partial or full replacement) executed by hello solution back end.</span></span>

<span data-ttu-id="2a0b8-223">所有 hello 先前執行的作業需要 hello **DeviceConnect**權限，如同 hello[安全性][ lnk-security]發行項。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-223">All hello preceding operations require hello **DeviceConnect** permission, as defined in hello [Security][lnk-security] article.</span></span>

<span data-ttu-id="2a0b8-224">hello [Azure IoT 裝置 Sdk] [ lnk-sdks]使其容易 toouse hello 前從多種語言和平台的作業。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-224">hello [Azure IoT device SDKs][lnk-sdks] make it easy toouse hello preceding operations from many languages and platforms.</span></span> <span data-ttu-id="2a0b8-225">Hello 的 IoT 中樞所需的內容同步處理基本類型的詳細資訊位於[裝置重新連線流程][lnk-reconnection]。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-225">More information on hello details of IoT Hub primitives for desired properties synchronization can be found in [Device reconnection flow][lnk-reconnection].</span></span>

> [!NOTE]
> <span data-ttu-id="2a0b8-226">目前，只連線 tooIoT 中樞的裝置可以存取裝置雙會使用 hello MQTT 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-226">Currently, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="2a0b8-227">參考主題：</span><span class="sxs-lookup"><span data-stu-id="2a0b8-227">Reference topics:</span></span>
<span data-ttu-id="2a0b8-228">hello 下列參考主題提供您有關控制存取 tooyour IoT 中樞的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-228">hello following reference topics provide you with more information about controlling access tooyour IoT hub.</span></span>

## <a name="tags-and-properties-format"></a><span data-ttu-id="2a0b8-229">標籤和屬性格式</span><span class="sxs-lookup"><span data-stu-id="2a0b8-229">Tags and properties format</span></span>
<span data-ttu-id="2a0b8-230">標記，想要的並報告的屬性是具有下列限制的 hello 的 JSON 物件：</span><span class="sxs-lookup"><span data-stu-id="2a0b8-230">Tags, desired, and reported properties are JSON objects with hello following restrictions:</span></span>

* <span data-ttu-id="2a0b8-231">JSON 物件中的所有索引鍵是區分大小寫的 64 個位元組的 UTF-8 UNICODE 字串。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-231">All keys in JSON objects are case-sensitive 64 bytes UTF-8 UNICODE strings.</span></span> <span data-ttu-id="2a0b8-232">允許的字元會排除 UNICODE 控制字元 (區段 C0 和 C1)，以及 `'.'`、`' '` 和 `'$'`。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-232">Allowed characters exclude UNICODE control characters (segments C0 and C1), and `'.'`, `' '`, and `'$'`.</span></span>
* <span data-ttu-id="2a0b8-233">JSON 物件中的所有值可以都是 hello 下列 JSON 型別： 布林值、 數字、 字串、 物件。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-233">All values in JSON objects can be of hello following JSON types: boolean, number, string, object.</span></span> <span data-ttu-id="2a0b8-234">不允許使用陣列。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-234">Arrays are not allowed.</span></span>
* <span data-ttu-id="2a0b8-235">標籤、所需屬性和報告屬性中所有 JSON 物件的深度上限為 5。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-235">All JSON objects in tags, desired, and reported properties can have a maximum depth of 5.</span></span> <span data-ttu-id="2a0b8-236">比方說，hello 接物件是有效的：</span><span class="sxs-lookup"><span data-stu-id="2a0b8-236">For instance, hello following object is valid:</span></span>

        {
            ...
            "tags": {
                "one": {
                    "two": {
                        "three": {
                            "four": {
                                "five": {
                                    "property": "value"
                                }
                            }
                        }
                    }
                }
            },
            ...
        }

* <span data-ttu-id="2a0b8-237">所有字串值的最大長度為 512 個位元組。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-237">All string values can be at most 512 bytes in length.</span></span>

## <a name="device-twin-size"></a><span data-ttu-id="2a0b8-238">裝置對應項大小</span><span class="sxs-lookup"><span data-stu-id="2a0b8-238">Device twin size</span></span>
<span data-ttu-id="2a0b8-239">IoT 中樞會強制執行 hello 值為 8 KB 大小限制`tags`， `properties/desired`，和`properties/reported`，排除唯讀項目。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-239">IoT Hub enforces an 8KB size limitation on hello values of `tags`, `properties/desired`, and `properties/reported`, excluding read-only elements.</span></span>
<span data-ttu-id="2a0b8-240">hello 大小的計算，來計算所有的字元不包括 UNICODE 控制字元 （區段 C0 和 C1） 和空間`' '`出現以外的字串常數時。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-240">hello size is computed by counting all characters excluding UNICODE control characters (segments C0 and C1) and space `' '` when it appears outside of a string constant.</span></span>
<span data-ttu-id="2a0b8-241">IoT 中樞拒絕，發生錯誤，會增加 hello 大小超過 hello 限制這些文件的所有作業。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-241">IoT Hub rejects with an error all operations that would increase hello size of those documents above hello limit.</span></span>

## <a name="device-twin-metadata"></a><span data-ttu-id="2a0b8-242">裝置對應項中繼資料</span><span class="sxs-lookup"><span data-stu-id="2a0b8-242">Device twin metadata</span></span>
<span data-ttu-id="2a0b8-243">IoT 中樞維護 hello 時間戳記的 hello 上次更新的每個 JSON 物件中裝置的兩個想要與報告的屬性。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-243">IoT Hub maintains hello timestamp of hello last update for each JSON object in device twin desired and reported properties.</span></span> <span data-ttu-id="2a0b8-244">hello 時間戳記都是 UTC 和編碼中 hello [ISO8601]格式`YYYY-MM-DDTHH:MM:SS.mmmZ`。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-244">hello timestamps are in UTC and encoded in hello [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span></span>
<span data-ttu-id="2a0b8-245">例如：</span><span class="sxs-lookup"><span data-stu-id="2a0b8-245">For example:</span></span>

        {
            ...
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": {
                                "$lastUpdated": "2016-03-30T16:24:48.789Z"
                            },
                            "$lastUpdated": "2016-03-30T16:24:48.789Z"
                        },
                        "$lastUpdated": "2016-03-30T16:24:48.789Z"
                    },
                    "$version": 23
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": "55%",
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": "5m",
                            "status": {
                                "$lastUpdated": "2016-03-31T16:35:48.789Z"
                            },
                            "$lastUpdated": "2016-03-31T16:35:48.789Z"
                        }
                        "batteryLevel": {
                            "$lastUpdated": "2016-04-01T16:35:48.789Z"
                        },
                        "$lastUpdated": "2016-04-01T16:24:48.789Z"
                    },
                    "$version": 123
                }
            }
            ...
        }

<span data-ttu-id="2a0b8-246">在物件索引鍵中移除每個層級 （hello JSON 結構的不只是 hello 分葉） toopreserve 更新保留這項資訊。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-246">This information is kept at every level (not just hello leaves of hello JSON structure) toopreserve updates that remove object keys.</span></span>

## <a name="optimistic-concurrency"></a><span data-ttu-id="2a0b8-247">開放式並行存取</span><span class="sxs-lookup"><span data-stu-id="2a0b8-247">Optimistic concurrency</span></span>
<span data-ttu-id="2a0b8-248">標籤、所需屬性和報告屬性全都支援開放式並行存取。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-248">Tags, desired, and reported properties all support optimistic concurrency.</span></span>
<span data-ttu-id="2a0b8-249">標記的 ETag，為每個有[RFC7232]，代表 hello 標記 JSON 表示法。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-249">Tags have an ETag, as per [RFC7232], that represents hello tag's JSON representation.</span></span> <span data-ttu-id="2a0b8-250">您可以從 hello 方案後端 tooensure 一致性的條件式更新作業中使用的 Etag。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-250">You can use ETags in conditional update operations from hello solution back end tooensure consistency.</span></span>

<span data-ttu-id="2a0b8-251">裝置的兩個想要與報告屬性沒有 Etag，但有`$version`保證 toobe 累加值。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-251">Device twin desired and reported properties do not have ETags, but have a `$version` value that is guaranteed toobe incremental.</span></span> <span data-ttu-id="2a0b8-252">同樣地 tooan hello 版本的 ETag，可供 hello 更新合作對象 tooenforce 一致性的更新。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-252">Similarly tooan ETag, hello version can be used by hello updating party tooenforce consistency of updates.</span></span> <span data-ttu-id="2a0b8-253">例如，裝置應用程式的報告屬性或 hello 方案後端所需的屬性。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-253">For example, a device app for a reported property or hello solution back end for a desired property.</span></span>

<span data-ttu-id="2a0b8-254">版本也很有用的當 observing 代理程式 （例如 hello 觀察 hello 預期屬性的裝置應用程式），必須協調 hello 作業的結果，擷取和更新通知之間的競爭情況。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-254">Versions are also useful when an observing agent (such as hello device app observing hello desired properties) must reconcile races between hello result of a retrieve operation and an update notification.</span></span> <span data-ttu-id="2a0b8-255">hello 區段[裝置重新連線流程][ lnk-reconnection]提供詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-255">hello section [Device reconnection flow][lnk-reconnection] provides more information.</span></span>

## <a name="device-reconnection-flow"></a><span data-ttu-id="2a0b8-256">裝置重新連線流程</span><span class="sxs-lookup"><span data-stu-id="2a0b8-256">Device reconnection flow</span></span>
<span data-ttu-id="2a0b8-257">IoT 中樞不會保留已中斷連線之裝置的所需屬性更新通知。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-257">IoT Hub does not preserve desired properties update notifications for disconnected devices.</span></span> <span data-ttu-id="2a0b8-258">它會遵循連接的裝置必須擷取 hello 完整的所需的內容的文件，在加法 toosubscribing 更新通知。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-258">It follows that a device that is connecting must retrieve hello full desired properties document, in addition toosubscribing for update notifications.</span></span> <span data-ttu-id="2a0b8-259">指定的更新通知和完整擷取之間的競爭情況的 hello 可能性，必須確保 hello 下列流程：</span><span class="sxs-lookup"><span data-stu-id="2a0b8-259">Given hello possibility of races between update notifications and full retrieval, hello following flow must be ensured:</span></span>

1. <span data-ttu-id="2a0b8-260">裝置應用程式會連接 tooan IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-260">Device app connects tooan IoT hub.</span></span>
2. <span data-ttu-id="2a0b8-261">裝置應用程式訂閱所需屬性更新通知。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-261">Device app subscribes for desired properties update notifications.</span></span>
3. <span data-ttu-id="2a0b8-262">裝置應用程式擷取 hello 需屬性的完整文件。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-262">Device app retrieves hello full document for desired properties.</span></span>

<span data-ttu-id="2a0b8-263">hello 裝置應用程式可以忽略所有通知使用`$version`小於或等於 hello hello 完整擷取的文件版本。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-263">hello device app can ignore all notifications with `$version` less or equal than hello version of hello full retrieved document.</span></span> <span data-ttu-id="2a0b8-264">IoT 中樞保證版本一定會遞增，因此這是可行的方法。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-264">This approach is possible because IoT Hub guarantees that versions always increment.</span></span>

> [!NOTE]
> <span data-ttu-id="2a0b8-265">Hello 中已實作此邏輯[Azure IoT 裝置 Sdk][lnk-sdks]。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-265">This logic is already implemented in hello [Azure IoT device SDKs][lnk-sdks].</span></span> <span data-ttu-id="2a0b8-266">只有當 hello 裝置應用程式無法使用任何 Azure IoT 裝置 Sdk，而且必須直接程式 hello MQTT 介面，這項描述會很有用。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-266">This description is useful only if hello device app cannot use any of Azure IoT device SDKs and must program hello MQTT interface directly.</span></span>
> 
> 

## <a name="additional-reference-material"></a><span data-ttu-id="2a0b8-267">其他參考資料</span><span class="sxs-lookup"><span data-stu-id="2a0b8-267">Additional reference material</span></span>
<span data-ttu-id="2a0b8-268">Hello IoT 中樞開發人員指南 》 中的其他參考主題包括：</span><span class="sxs-lookup"><span data-stu-id="2a0b8-268">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="2a0b8-269">hello [IoT 中樞端點][ lnk-endpoints]文章說明 hello 各種執行階段和管理作業的每個 IoT 中樞會公開的端點。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-269">hello [IoT Hub endpoints][lnk-endpoints] article describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="2a0b8-270">hello[節流和配額][ lnk-quotas]文章說明 hello 配額套用 toohello IoT 中心服務和 hello 節流行為 tooexpect，當您使用 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-270">hello [Throttling and quotas][lnk-quotas] article describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="2a0b8-271">hello [Azure IoT 裝置和服務 Sdk] [ lnk-sdks]文章列出 hello 互動的裝置和服務應用程式開發與 IoT 中樞時，您可以使用各種語言 Sdk。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-271">hello [Azure IoT device and service SDKs][lnk-sdks] article lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="2a0b8-272">hello[裝置雙、 作業和訊息路由的 IoT 中樞查詢語言][ lnk-query]文章說明 hello IoT 中樞的查詢語言，您可以使用您的裝置雙和作業相關的 tooretrieve 資訊從 IoT 中樞.</span><span class="sxs-lookup"><span data-stu-id="2a0b8-272">hello [IoT Hub query language for device twins, jobs, and message routing][lnk-query] article describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="2a0b8-273">hello [IoT 中樞 MQTT 支援][ lnk-devguide-mqtt]文章提供 IoT 中樞支援 hello MQTT 通訊協定的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="2a0b8-273">hello [IoT Hub MQTT support][lnk-devguide-mqtt] article provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a0b8-274">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2a0b8-274">Next steps</span></span>
<span data-ttu-id="2a0b8-275">現在您已經學會有關裝置雙，您可能想要遵循 IoT 中樞開發人員指南主題 hello:</span><span class="sxs-lookup"><span data-stu-id="2a0b8-275">Now you have learned about device twins, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="2a0b8-276">[在裝置上叫用直接方法][lnk-methods]</span><span class="sxs-lookup"><span data-stu-id="2a0b8-276">[Invoke a direct method on a device][lnk-methods]</span></span>
* <span data-ttu-id="2a0b8-277">[排程多個裝置上的作業][lnk-jobs]</span><span class="sxs-lookup"><span data-stu-id="2a0b8-277">[Schedule jobs on multiple devices][lnk-jobs]</span></span>

<span data-ttu-id="2a0b8-278">如果您想要查看這篇文章中所述的 hello 概念 tootry，您可能想要遵循 IoT 中樞教學課程的 hello:</span><span class="sxs-lookup"><span data-stu-id="2a0b8-278">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorials:</span></span>

* <span data-ttu-id="2a0b8-279">[如何 toouse hello 裝置兩個][lnk-twin-tutorial]</span><span class="sxs-lookup"><span data-stu-id="2a0b8-279">[How toouse hello device twin][lnk-twin-tutorial]</span></span>
* <span data-ttu-id="2a0b8-280">[如何 toouse 裝置 twin 屬性][lnk-twin-properties]</span><span class="sxs-lookup"><span data-stu-id="2a0b8-280">[How toouse device twin properties][lnk-twin-properties]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-identity]: iot-hub-devguide-identity-registry.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-security]: iot-hub-devguide-security.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[ISO8601]: https://en.wikipedia.org/wiki/ISO_8601
[RFC7232]: https://tools.ietf.org/html/rfc7232
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-twin-metadata]: iot-hub-devguide-device-twins.md#device-twin-metadata
[lnk-concurrency]: iot-hub-devguide-device-twins.md#optimistic-concurrency
[lnk-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow

[img-twin]: media/iot-hub-devguide-device-twins/twin.png
