---
title: "了解 Azure IoT 中樞裝置對應項 | Microsoft Docs"
description: "開發人員指南 - 使用裝置對應項同步處理 IoT 中樞與裝置之間的狀態和組態資料"
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
ms.openlocfilehash: b316aa419d558547f90a914a22fb29935076de21
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a><span data-ttu-id="09a6b-103">了解和使用 Azure IoT 中樞的裝置對應項</span><span class="sxs-lookup"><span data-stu-id="09a6b-103">Understand and use device twins in IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="09a6b-104">概觀</span><span class="sxs-lookup"><span data-stu-id="09a6b-104">Overview</span></span>
<span data-ttu-id="09a6b-105">「裝置對應項」是存放裝置狀態資訊 (中繼資料、組態和條件) 的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="09a6b-105">*Device twins* are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="09a6b-106">IoT 中樞會為連線到 IoT 中樞的每個裝置保存裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="09a6b-106">IoT Hub persists a device twin for each device that you connect to IoT Hub.</span></span> <span data-ttu-id="09a6b-107">本文章說明：</span><span class="sxs-lookup"><span data-stu-id="09a6b-107">This article describes:</span></span>

* <span data-ttu-id="09a6b-108">裝置對應項的結構︰標籤、所需屬性和報告屬性，以及</span><span class="sxs-lookup"><span data-stu-id="09a6b-108">The structure of the device twin: *tags*, *desired* and *reported properties*, and</span></span>
* <span data-ttu-id="09a6b-109">裝置應用程式和後端可以對裝置對應項執行的作業。</span><span class="sxs-lookup"><span data-stu-id="09a6b-109">The operations that device apps and back ends can perform on device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="09a6b-110">目前，裝置對應項只能從使用 MQTT 通訊協定連線至 IoT 中樞的裝置存取。</span><span class="sxs-lookup"><span data-stu-id="09a6b-110">Currently, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span> <span data-ttu-id="09a6b-111">請參閱 [MQTT 支援][lnk-devguide-mqtt]文章，以取得如何將現有裝置應用程式轉換為使用 MQTT 的指示。</span><span class="sxs-lookup"><span data-stu-id="09a6b-111">Refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.</span></span>
> 
> 

### <a name="when-to-use"></a><span data-ttu-id="09a6b-112">使用時機</span><span class="sxs-lookup"><span data-stu-id="09a6b-112">When to use</span></span>
<span data-ttu-id="09a6b-113">使用裝置對應項可以：</span><span class="sxs-lookup"><span data-stu-id="09a6b-113">Use device twins to:</span></span>

* <span data-ttu-id="09a6b-114">在雲端儲存裝置特定的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="09a6b-114">Store device-specific metadata in the cloud.</span></span> <span data-ttu-id="09a6b-115">例如，販賣機的部署位置。</span><span class="sxs-lookup"><span data-stu-id="09a6b-115">For example, the deployment location of a vending machine.</span></span>
* <span data-ttu-id="09a6b-116">從您的裝置應用程式報告目前狀態資訊，例如可用功能和狀況。</span><span class="sxs-lookup"><span data-stu-id="09a6b-116">Report current state information such as available capabilities and conditions from your device app.</span></span> <span data-ttu-id="09a6b-117">例如，裝置會透過行動電話或 WiFi 連線到您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="09a6b-117">For example, a device is connected to your IoT hub over cellular or WiFi.</span></span>
* <span data-ttu-id="09a6b-118">同步處理裝置與後端應用程式之間長時間執行之工作流程的狀態。</span><span class="sxs-lookup"><span data-stu-id="09a6b-118">Synchronize the state of long-running workflows between device app and back-end app.</span></span> <span data-ttu-id="09a6b-119">例如，當解決方案後端指定要安裝的新韌體版本時，以及裝置應用程式報告更新處理程序的各個階段時。</span><span class="sxs-lookup"><span data-stu-id="09a6b-119">For example, when the solution back end specifies the new firmware version to install, and the device app reports the various stages of the update process.</span></span>
* <span data-ttu-id="09a6b-120">查詢裝置中繼資料、組態或狀態。</span><span class="sxs-lookup"><span data-stu-id="09a6b-120">Query your device metadata, configuration, or state.</span></span>

<span data-ttu-id="09a6b-121">請參閱[裝置到雲端通訊指引][lnk-d2c-guidance]，以取得有關使用報告屬性、裝置到雲端訊息或檔案上傳的指引。</span><span class="sxs-lookup"><span data-stu-id="09a6b-121">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] for guidance on using reported properties, device-to-cloud messages, or file upload.</span></span>
<span data-ttu-id="09a6b-122">請參閱[雲端對裝置通訊指引][lnk-c2d-guidance]，以取得有關使用所需屬性、直接方法或雲端到裝置訊息的指引。</span><span class="sxs-lookup"><span data-stu-id="09a6b-122">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] for guidance on using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="device-twins"></a><span data-ttu-id="09a6b-123">裝置對應項</span><span class="sxs-lookup"><span data-stu-id="09a6b-123">Device twins</span></span>
<span data-ttu-id="09a6b-124">裝置對應項會儲存裝置相關資訊，以供︰</span><span class="sxs-lookup"><span data-stu-id="09a6b-124">Device twins store device-related information that:</span></span>

* <span data-ttu-id="09a6b-125">裝置和後端用來同步處理裝置的狀況和組態。</span><span class="sxs-lookup"><span data-stu-id="09a6b-125">Device and back ends can use to synchronize device conditions and configuration.</span></span>
* <span data-ttu-id="09a6b-126">解決方案後端用來查詢和鎖定長時間執行的作業。</span><span class="sxs-lookup"><span data-stu-id="09a6b-126">The solution back end can use to query and target long-running operations.</span></span>

<span data-ttu-id="09a6b-127">裝置對應項的生命週期會連結至對應的[裝置身分識別][lnk-identity]。</span><span class="sxs-lookup"><span data-stu-id="09a6b-127">The lifecycle of a device twin is linked to the corresponding [device identity][lnk-identity].</span></span> <span data-ttu-id="09a6b-128">在 IoT 中樞建立或刪除新的裝置身分識別時，會隱含地建立和刪除裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="09a6b-128">Device twins are implicitly created and deleted when a new device identity is created or deleted in IoT Hub.</span></span>

<span data-ttu-id="09a6b-129">裝置的兩個是 JSON 文件，其中含有︰</span><span class="sxs-lookup"><span data-stu-id="09a6b-129">A device twin is a JSON document that includes:</span></span>

* <span data-ttu-id="09a6b-130">**標籤**。</span><span class="sxs-lookup"><span data-stu-id="09a6b-130">**Tags**.</span></span> <span data-ttu-id="09a6b-131">解決方案後端可以讀取及寫入的 JSON 文件區段。</span><span class="sxs-lookup"><span data-stu-id="09a6b-131">A section of the JSON document that the solution back end can read from and write to.</span></span> <span data-ttu-id="09a6b-132">裝置應用程式看不到標籤。</span><span class="sxs-lookup"><span data-stu-id="09a6b-132">Tags are not visible to device apps.</span></span>
* <span data-ttu-id="09a6b-133">**所需屬性**。</span><span class="sxs-lookup"><span data-stu-id="09a6b-133">**Desired properties**.</span></span> <span data-ttu-id="09a6b-134">搭配報告屬性使用，以便同步處理裝置的組態或狀況。</span><span class="sxs-lookup"><span data-stu-id="09a6b-134">Used along with reported properties to synchronize device configuration or conditions.</span></span> <span data-ttu-id="09a6b-135">所需屬性只能由解決方案後端設定，且可供裝置應用程式讀取。</span><span class="sxs-lookup"><span data-stu-id="09a6b-135">Desired properties can only be set by the solution back end and can be read by the device app.</span></span> <span data-ttu-id="09a6b-136">所需屬性有所變更時，裝置應用程式也可以即時收到通知。</span><span class="sxs-lookup"><span data-stu-id="09a6b-136">The device app can also be notified in real time of changes in the desired properties.</span></span>
* <span data-ttu-id="09a6b-137">**報告屬性**。</span><span class="sxs-lookup"><span data-stu-id="09a6b-137">**Reported properties**.</span></span> <span data-ttu-id="09a6b-138">搭配所需屬性使用，以便同步處理裝置的組態或狀況。</span><span class="sxs-lookup"><span data-stu-id="09a6b-138">Used along with desired properties to synchronize device configuration or conditions.</span></span> <span data-ttu-id="09a6b-139">報告屬性只能由裝置應用程式設定，且可供解決方案後端讀取和查詢。</span><span class="sxs-lookup"><span data-stu-id="09a6b-139">Reported properties can only be set by the device app and can be read and queried by the solution back end.</span></span>

<span data-ttu-id="09a6b-140">此外，裝置對應項 JSON 文件的根目錄包含來自[身分識別登錄][lnk-identity]中儲存之對應身分識別的唯讀屬性。</span><span class="sxs-lookup"><span data-stu-id="09a6b-140">Additionally, the root of the device twin JSON document contains the read-only properties from the corresponding device identity stored in the [identity registry][lnk-identity].</span></span>

![][img-twin]

<span data-ttu-id="09a6b-141">以下範例顯示裝置對應項 JSON 文件︰</span><span class="sxs-lookup"><span data-stu-id="09a6b-141">The following example shows a device twin JSON document:</span></span>

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

<span data-ttu-id="09a6b-142">在根物件中，都是系統屬性，並且是 `tags` 以及 `reported` 和 `desired` 屬性的容器物件。</span><span class="sxs-lookup"><span data-stu-id="09a6b-142">In the root object, are the system properties, and container objects for `tags` and both `reported` and `desired` properties.</span></span> <span data-ttu-id="09a6b-143">`properties` 容器包含一些唯讀元素 (`$metadata`、`$etag` 和 `$version`)，其說明位於[裝置對應項中繼資料][lnk-twin-metadata]和[開放式並行存取][lnk-concurrency]章節。</span><span class="sxs-lookup"><span data-stu-id="09a6b-143">The `properties` container contains some read-only elements (`$metadata`, `$etag`, and `$version`) described in the [Device twin metadata][lnk-twin-metadata] and [Optimistic concurrency][lnk-concurrency] sections.</span></span>

### <a name="reported-property-example"></a><span data-ttu-id="09a6b-144">報告屬性範例</span><span class="sxs-lookup"><span data-stu-id="09a6b-144">Reported property example</span></span>
<span data-ttu-id="09a6b-145">在上述範例中，裝置對應項包含由裝置應用程式所報告的 `batteryLevel` 屬性。</span><span class="sxs-lookup"><span data-stu-id="09a6b-145">In the previous example, the device twin contains a `batteryLevel` property that is reported by the device app.</span></span> <span data-ttu-id="09a6b-146">此屬性可讓您根據最後一次報告的電池電量對裝置進行查詢和操作。</span><span class="sxs-lookup"><span data-stu-id="09a6b-146">This property makes it possible to query and operate on devices based on the last reported battery level.</span></span> <span data-ttu-id="09a6b-147">其他範例包含裝置應用程式報告功能或連線能力選項。</span><span class="sxs-lookup"><span data-stu-id="09a6b-147">Other examples include the device app reporting device capabilities or connectivity options.</span></span>

> [!NOTE]
> <span data-ttu-id="09a6b-148">當解決方案後端想要取得屬性的最後已知值時，報告屬性如何簡化這種情況。</span><span class="sxs-lookup"><span data-stu-id="09a6b-148">Reported properties simplify scenarios where the solution back end is interested in the last known value of a property.</span></span> <span data-ttu-id="09a6b-149">如果解決方案後端需要以一連串時間戳記事件 (例如時間序列) 的形式處理裝置遙測，請使用[裝置到雲端訊息][lnk-d2c]。</span><span class="sxs-lookup"><span data-stu-id="09a6b-149">Use [device-to-cloud messages][lnk-d2c] if the solution back end needs to process device telemetry in the form of sequences of timestamped events, such as time series.</span></span>

### <a name="desired-property-example"></a><span data-ttu-id="09a6b-150">所需屬性範例</span><span class="sxs-lookup"><span data-stu-id="09a6b-150">Desired property example</span></span>
<span data-ttu-id="09a6b-151">在上述範例中，解決方案後端和裝置應用程式會使用 `telemetryConfig` 裝置對應項的所需屬性和報告屬性，以同步處理此裝置的遙測組態。</span><span class="sxs-lookup"><span data-stu-id="09a6b-151">In the previous example, the `telemetryConfig` device twin desired and reported properties are used by the solution back end and the device app to synchronize the telemetry configuration for this device.</span></span> <span data-ttu-id="09a6b-152">例如：</span><span class="sxs-lookup"><span data-stu-id="09a6b-152">For example:</span></span>

1. <span data-ttu-id="09a6b-153">解決方案後端會以所需組態值來設定所需屬性。</span><span class="sxs-lookup"><span data-stu-id="09a6b-153">The solution back end sets the desired property with the desired configuration value.</span></span> <span data-ttu-id="09a6b-154">以下是含有所需屬性集的文件部分︰</span><span class="sxs-lookup"><span data-stu-id="09a6b-154">Here is the portion of the document with the desired property set:</span></span>
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. <span data-ttu-id="09a6b-155">裝置應用程式會在已連線或第一次重新連線時，立即收到變更通知。</span><span class="sxs-lookup"><span data-stu-id="09a6b-155">The device app is notified of the change immediately if connected, or at the first reconnect.</span></span> <span data-ttu-id="09a6b-156">裝置應用程式接著會報告更新的組態 (或使用 `status` 屬性的錯誤狀況)。</span><span class="sxs-lookup"><span data-stu-id="09a6b-156">The device app then reports the updated configuration (or an error condition using the `status` property).</span></span> <span data-ttu-id="09a6b-157">以下是報告屬性的部分︰</span><span class="sxs-lookup"><span data-stu-id="09a6b-157">Here is the portion of the reported properties:</span></span>
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. <span data-ttu-id="09a6b-158">解決方案後端可以[查詢][lnk-query]裝置對應項，以追蹤組態作業在許多裝置上的結果。</span><span class="sxs-lookup"><span data-stu-id="09a6b-158">The solution back end can track the results of the configuration operation across many devices, by [querying][lnk-query] device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="09a6b-159">上述程式碼片段舉例說明了用來編碼裝置組態和其狀態的方式，為了方便閱讀，其內容已經過最佳化。</span><span class="sxs-lookup"><span data-stu-id="09a6b-159">The preceding snippets are examples, optimized for readability, of one way to encode a device configuration and its status.</span></span> <span data-ttu-id="09a6b-160">IoT 中樞不會對裝置對應項中的裝置對應項所需屬性和報告屬性強制實行特定結構描述。</span><span class="sxs-lookup"><span data-stu-id="09a6b-160">IoT Hub does not impose a specific schema for the device twin desired and reported properties in the device twins.</span></span>
> 
> 

<span data-ttu-id="09a6b-161">您可以使用裝置對應項來同步處理長時間執行的作業，例如韌體更新。</span><span class="sxs-lookup"><span data-stu-id="09a6b-161">You can use twins to synchronize long-running operations such as firmware updates.</span></span> <span data-ttu-id="09a6b-162">如需如何使用屬性來跨裝置同步處理及追蹤長時間執行的作業，請參閱[使用所需屬性來設定裝置][lnk-twin-properties]。</span><span class="sxs-lookup"><span data-stu-id="09a6b-162">For more information on how to use properties to synchronize and track a long running operation across devices, see [Use desired properties to configure devices][lnk-twin-properties].</span></span>

## <a name="back-end-operations"></a><span data-ttu-id="09a6b-163">後端作業</span><span class="sxs-lookup"><span data-stu-id="09a6b-163">Back-end operations</span></span>
<span data-ttu-id="09a6b-164">解決方案後端會使用下列不可部分完成的作業 (透過 HTTP 公開) 來操作裝置對應項︰</span><span class="sxs-lookup"><span data-stu-id="09a6b-164">The solution back end operates on the device twin using the following atomic operations, exposed through HTTP:</span></span>

1. <span data-ttu-id="09a6b-165">**依識別碼擷取裝置對應項**。此作業會傳回裝置對應項文件，包括標籤以及所需屬性、報告屬性和系統屬性。</span><span class="sxs-lookup"><span data-stu-id="09a6b-165">**Retrieve device twin by id**. This operation returns the device twin document, including tags and desired, reported, and system properties.</span></span>
2. <span data-ttu-id="09a6b-166">**部份更新裝置對應項**。</span><span class="sxs-lookup"><span data-stu-id="09a6b-166">**Partially update device twin**.</span></span> <span data-ttu-id="09a6b-167">此作業可讓解決方案後端局部地更新裝置對應項中的標籤或所需屬性。</span><span class="sxs-lookup"><span data-stu-id="09a6b-167">This operation enables the solution back end to partially update the tags or desired properties in a device twin.</span></span> <span data-ttu-id="09a6b-168">部分更新會以 JSON 文件的形式來表示，以新增或更新任何屬性。</span><span class="sxs-lookup"><span data-stu-id="09a6b-168">The partial update is expressed as a JSON document that adds or updates any property.</span></span> <span data-ttu-id="09a6b-169">設定為 `null` 的屬性會遭到移除。</span><span class="sxs-lookup"><span data-stu-id="09a6b-169">Properties set to `null` are removed.</span></span> <span data-ttu-id="09a6b-170">下列範例會以 `{"newProperty": "newValue"}` 值建立新的所需屬性、以 `"otherNewValue"` 覆寫 `existingProperty` 的現有值，並移除 `otherOldProperty`。</span><span class="sxs-lookup"><span data-stu-id="09a6b-170">The following example creates a new desired property with value `{"newProperty": "newValue"}`, overwrites the existing value of `existingProperty` with `"otherNewValue"`, and removes `otherOldProperty`.</span></span> <span data-ttu-id="09a6b-171">不會對現有的所需屬性或標籤進行任何變更︰</span><span class="sxs-lookup"><span data-stu-id="09a6b-171">No other changes are made to existing desired properties or tags:</span></span>
   
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
3. <span data-ttu-id="09a6b-172">**取代所需屬性**。</span><span class="sxs-lookup"><span data-stu-id="09a6b-172">**Replace desired properties**.</span></span> <span data-ttu-id="09a6b-173">此作業可讓解決方案後端完全覆寫所有現有的所需屬性，並以新的 JSON 文件取代 `properties/desired`。</span><span class="sxs-lookup"><span data-stu-id="09a6b-173">This operation enables the solution back end to completely overwrite all existing desired properties and substitute a new JSON document for `properties/desired`.</span></span>
4. <span data-ttu-id="09a6b-174">**取代標籤**。</span><span class="sxs-lookup"><span data-stu-id="09a6b-174">**Replace tags**.</span></span> <span data-ttu-id="09a6b-175">此作業可讓解決方案後端完全覆寫所有現有的標籤，並以新的 JSON 文件取代 `tags`。</span><span class="sxs-lookup"><span data-stu-id="09a6b-175">This operation enables the solution back end to completely overwrite all existing tags and substitute a new JSON document for `tags`.</span></span>
5. <span data-ttu-id="09a6b-176">**接收對應項通知**。</span><span class="sxs-lookup"><span data-stu-id="09a6b-176">**Receive twin notifications**.</span></span> <span data-ttu-id="09a6b-177">這項作業可以在對應項修改時通知方案後端。</span><span class="sxs-lookup"><span data-stu-id="09a6b-177">This operation allows the solution back end to be notified when the twin is modified.</span></span> <span data-ttu-id="09a6b-178">若要這樣做，您的 IoT 解決方案必須建立路由，並將資料來源設為等於 *twinChangeEvents*。</span><span class="sxs-lookup"><span data-stu-id="09a6b-178">To do so, your IoT solution needs to create a route and to set the Data Source equal to *twinChangeEvents*.</span></span> <span data-ttu-id="09a6b-179">根據預設，不會傳送任何對應項通知，亦即預先不存在這類路由。</span><span class="sxs-lookup"><span data-stu-id="09a6b-179">By default, no twin notifications are sent, that is, no such routes pre-exist.</span></span> <span data-ttu-id="09a6b-180">如果變更率太高，或基於其他原因，例如內部失敗，IoT 中樞可能只會傳送一個包含所有變更的通知。</span><span class="sxs-lookup"><span data-stu-id="09a6b-180">If the rate of change is too high, or for other reasons, such as internal failures, the IoT Hub might send only one notification that contains all changes.</span></span> <span data-ttu-id="09a6b-181">因此，如果您的應用程式需要可靠地稽核和記錄所有中間狀態，則仍建議您使用 D2C 訊息。</span><span class="sxs-lookup"><span data-stu-id="09a6b-181">So, if your application needs reliable auditing and logging of all intermediate states, then it is still recommended that you use D2C messages.</span></span> <span data-ttu-id="09a6b-182">對應項通知訊息包含屬性和內文。</span><span class="sxs-lookup"><span data-stu-id="09a6b-182">The twin notification message includes properties, and body.</span></span>

    - <span data-ttu-id="09a6b-183">屬性</span><span class="sxs-lookup"><span data-stu-id="09a6b-183">Properties</span></span>

    | <span data-ttu-id="09a6b-184">名稱</span><span class="sxs-lookup"><span data-stu-id="09a6b-184">Name</span></span> | <span data-ttu-id="09a6b-185">值</span><span class="sxs-lookup"><span data-stu-id="09a6b-185">Value</span></span> |
    | --- | --- |
    <span data-ttu-id="09a6b-186">$content-type</span><span class="sxs-lookup"><span data-stu-id="09a6b-186">$content-type</span></span> | <span data-ttu-id="09a6b-187">application/json</span><span class="sxs-lookup"><span data-stu-id="09a6b-187">application/json</span></span> |
    <span data-ttu-id="09a6b-188">$iothub-enqueuedtime</span><span class="sxs-lookup"><span data-stu-id="09a6b-188">$iothub-enqueuedtime</span></span> |  <span data-ttu-id="09a6b-189">傳送通知的時間</span><span class="sxs-lookup"><span data-stu-id="09a6b-189">Time when the notification was sent</span></span> |
    <span data-ttu-id="09a6b-190">$iothub-message-source</span><span class="sxs-lookup"><span data-stu-id="09a6b-190">$iothub-message-source</span></span> | <span data-ttu-id="09a6b-191">twinChangeEvents</span><span class="sxs-lookup"><span data-stu-id="09a6b-191">twinChangeEvents</span></span> |
    <span data-ttu-id="09a6b-192">$content-encoding</span><span class="sxs-lookup"><span data-stu-id="09a6b-192">$content-encoding</span></span> | <span data-ttu-id="09a6b-193">utf-8</span><span class="sxs-lookup"><span data-stu-id="09a6b-193">utf-8</span></span> |
    <span data-ttu-id="09a6b-194">deviceId</span><span class="sxs-lookup"><span data-stu-id="09a6b-194">deviceId</span></span> | <span data-ttu-id="09a6b-195">裝置識別碼</span><span class="sxs-lookup"><span data-stu-id="09a6b-195">Id of the device</span></span> |
    <span data-ttu-id="09a6b-196">hubName</span><span class="sxs-lookup"><span data-stu-id="09a6b-196">hubName</span></span> | <span data-ttu-id="09a6b-197">IoT 中樞名稱</span><span class="sxs-lookup"><span data-stu-id="09a6b-197">Name of IoT Hub</span></span> |
    <span data-ttu-id="09a6b-198">operationTimestamp</span><span class="sxs-lookup"><span data-stu-id="09a6b-198">operationTimestamp</span></span> | <span data-ttu-id="09a6b-199">作業的 [ISO8601] 時間戳記</span><span class="sxs-lookup"><span data-stu-id="09a6b-199">[ISO8601] timestamp of operation</span></span> |
    <span data-ttu-id="09a6b-200">iothub-message-schema</span><span class="sxs-lookup"><span data-stu-id="09a6b-200">iothub-message-schema</span></span> | <span data-ttu-id="09a6b-201">deviceLifecycleNotification</span><span class="sxs-lookup"><span data-stu-id="09a6b-201">deviceLifecycleNotification</span></span> |
    <span data-ttu-id="09a6b-202">opType</span><span class="sxs-lookup"><span data-stu-id="09a6b-202">opType</span></span> | <span data-ttu-id="09a6b-203">"replaceTwin" 或 "updateTwin"</span><span class="sxs-lookup"><span data-stu-id="09a6b-203">"replaceTwin" or "updateTwin"</span></span> |

    <span data-ttu-id="09a6b-204">訊息系統屬性前面會加上 `'$'` 符號。</span><span class="sxs-lookup"><span data-stu-id="09a6b-204">Message system properties are prefixed with the `'$'` symbol.</span></span>

    - <span data-ttu-id="09a6b-205">body</span><span class="sxs-lookup"><span data-stu-id="09a6b-205">Body</span></span>
        
    <span data-ttu-id="09a6b-206">本節包含所有對應項變更 (JSON 格式)。</span><span class="sxs-lookup"><span data-stu-id="09a6b-206">This section includes all the twin changes in a JSON format.</span></span> <span data-ttu-id="09a6b-207">它使用的格式與修補程式的格式相同，差別在於它可以包含所有對應項區段︰tags、properties.reported、properties.desired，而且包含 “$metadata” 項目。</span><span class="sxs-lookup"><span data-stu-id="09a6b-207">It uses the same format as a patch, with the difference that it can contain all twin sections: tags, properties.reported, properties.desired, and that it contains the “$metadata” elements.</span></span> <span data-ttu-id="09a6b-208">例如，</span><span class="sxs-lookup"><span data-stu-id="09a6b-208">For example,</span></span>
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

<span data-ttu-id="09a6b-209">上述所有作業皆支援[開放式並行存取][lnk-concurrency]，而且需要 **ServiceConnect** 權限，如[安全性][lnk-security]一文所定義。</span><span class="sxs-lookup"><span data-stu-id="09a6b-209">All the preceding operations support [Optimistic concurrency][lnk-concurrency] and require the **ServiceConnect** permission, as defined in the [Security][lnk-security] article.</span></span>

<span data-ttu-id="09a6b-210">除了這些作業，解決方案後端還可以︰</span><span class="sxs-lookup"><span data-stu-id="09a6b-210">In addition to these operations, the solution back end can:</span></span>

* <span data-ttu-id="09a6b-211">使用類似 SQL 的 [IoT 中樞查詢語言][lnk-query]來查詢裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="09a6b-211">Query the device twins using the SQL-like [IoT Hub query language][lnk-query].</span></span>
* <span data-ttu-id="09a6b-212">使用[作業][lnk-jobs]在大型裝置對應項集合上執行作業。</span><span class="sxs-lookup"><span data-stu-id="09a6b-212">Perform operations on large sets of device twins using [jobs][lnk-jobs].</span></span>

## <a name="device-operations"></a><span data-ttu-id="09a6b-213">裝置作業</span><span class="sxs-lookup"><span data-stu-id="09a6b-213">Device operations</span></span>
<span data-ttu-id="09a6b-214">裝置應用程式會使用下列不可部分完成的作業來操作裝置對應項︰</span><span class="sxs-lookup"><span data-stu-id="09a6b-214">The device app operates on the device twin using the following atomic operations:</span></span>

1. <span data-ttu-id="09a6b-215">**擷取裝置對應項**。</span><span class="sxs-lookup"><span data-stu-id="09a6b-215">**Retrieve device twin**.</span></span> <span data-ttu-id="09a6b-216">此作業會針對目前連線的裝置傳回裝置對應項文件 (包括標籤以及所需屬性、報告屬性和系統屬性)。</span><span class="sxs-lookup"><span data-stu-id="09a6b-216">This operation returns the device twin document (including tags and desired, reported and system properties) for the currently connected device.</span></span>
2. <span data-ttu-id="09a6b-217">**部分更新的報告屬性**。</span><span class="sxs-lookup"><span data-stu-id="09a6b-217">**Partially update reported properties**.</span></span> <span data-ttu-id="09a6b-218">此作業可針對目前連線裝置的報告屬性進行部分更新。</span><span class="sxs-lookup"><span data-stu-id="09a6b-218">This operation enables the partial update of the reported properties of the currently connected device.</span></span> <span data-ttu-id="09a6b-219">此作業使用的 JSON 更新格式，與解決方案後端用於局部更新所需屬性的格式相同。</span><span class="sxs-lookup"><span data-stu-id="09a6b-219">This operation uses the same JSON update format that the solution back end uses for a partial update of desired properties.</span></span>
3. <span data-ttu-id="09a6b-220">**觀察所需屬性**。</span><span class="sxs-lookup"><span data-stu-id="09a6b-220">**Observe desired properties**.</span></span> <span data-ttu-id="09a6b-221">目前連線的裝置可以選擇在所需屬性進行更新時收到通知。</span><span class="sxs-lookup"><span data-stu-id="09a6b-221">The currently connected device can choose to be notified of updates to the desired properties when they happen.</span></span> <span data-ttu-id="09a6b-222">裝置會收到由解決方案後端執行的相同更新形式 (部分或完整取代)。</span><span class="sxs-lookup"><span data-stu-id="09a6b-222">The device receives the same form of update (partial or full replacement) executed by the solution back end.</span></span>

<span data-ttu-id="09a6b-223">上述所有作業都需要 **DeviceConnect** 權限，如[安全性][lnk-security]一文所定義。</span><span class="sxs-lookup"><span data-stu-id="09a6b-223">All the preceding operations require the **DeviceConnect** permission, as defined in the [Security][lnk-security] article.</span></span>

<span data-ttu-id="09a6b-224">[Azure IoT 裝置 SDK][lnk-sdks] 可讓您透過許多語言和平台輕鬆使用上述作業。</span><span class="sxs-lookup"><span data-stu-id="09a6b-224">The [Azure IoT device SDKs][lnk-sdks] make it easy to use the preceding operations from many languages and platforms.</span></span> <span data-ttu-id="09a6b-225">如需 IoT 中樞之所需屬性同步處理基元的詳細資訊，請參閱[裝置重新連線流程][lnk-reconnection]。</span><span class="sxs-lookup"><span data-stu-id="09a6b-225">More information on the details of IoT Hub primitives for desired properties synchronization can be found in [Device reconnection flow][lnk-reconnection].</span></span>

> [!NOTE]
> <span data-ttu-id="09a6b-226">目前，裝置對應項只能從使用 MQTT 通訊協定連線至 IoT 中樞的裝置存取。</span><span class="sxs-lookup"><span data-stu-id="09a6b-226">Currently, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="09a6b-227">參考主題：</span><span class="sxs-lookup"><span data-stu-id="09a6b-227">Reference topics:</span></span>
<span data-ttu-id="09a6b-228">下列參考主題會提供您關於控制 IoT 中樞存取權的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="09a6b-228">The following reference topics provide you with more information about controlling access to your IoT hub.</span></span>

## <a name="tags-and-properties-format"></a><span data-ttu-id="09a6b-229">標籤和屬性格式</span><span class="sxs-lookup"><span data-stu-id="09a6b-229">Tags and properties format</span></span>
<span data-ttu-id="09a6b-230">標籤、所需屬性和報告屬性是具有下列限制的 JSON 物件︰</span><span class="sxs-lookup"><span data-stu-id="09a6b-230">Tags, desired, and reported properties are JSON objects with the following restrictions:</span></span>

* <span data-ttu-id="09a6b-231">JSON 物件中的所有索引鍵是區分大小寫的 64 個位元組的 UTF-8 UNICODE 字串。</span><span class="sxs-lookup"><span data-stu-id="09a6b-231">All keys in JSON objects are case-sensitive 64 bytes UTF-8 UNICODE strings.</span></span> <span data-ttu-id="09a6b-232">允許的字元會排除 UNICODE 控制字元 (區段 C0 和 C1)，以及 `'.'`、`' '` 和 `'$'`。</span><span class="sxs-lookup"><span data-stu-id="09a6b-232">Allowed characters exclude UNICODE control characters (segments C0 and C1), and `'.'`, `' '`, and `'$'`.</span></span>
* <span data-ttu-id="09a6b-233">JSON 物件中的所有值可以屬於下列 JSON 類型︰布林值、數字、字串、物件。</span><span class="sxs-lookup"><span data-stu-id="09a6b-233">All values in JSON objects can be of the following JSON types: boolean, number, string, object.</span></span> <span data-ttu-id="09a6b-234">不允許使用陣列。</span><span class="sxs-lookup"><span data-stu-id="09a6b-234">Arrays are not allowed.</span></span>
* <span data-ttu-id="09a6b-235">標籤、所需屬性和報告屬性中所有 JSON 物件的深度上限為 5。</span><span class="sxs-lookup"><span data-stu-id="09a6b-235">All JSON objects in tags, desired, and reported properties can have a maximum depth of 5.</span></span> <span data-ttu-id="09a6b-236">例如，下列物件有效：</span><span class="sxs-lookup"><span data-stu-id="09a6b-236">For instance, the following object is valid:</span></span>

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

* <span data-ttu-id="09a6b-237">所有字串值的最大長度為 512 個位元組。</span><span class="sxs-lookup"><span data-stu-id="09a6b-237">All string values can be at most 512 bytes in length.</span></span>

## <a name="device-twin-size"></a><span data-ttu-id="09a6b-238">裝置對應項大小</span><span class="sxs-lookup"><span data-stu-id="09a6b-238">Device twin size</span></span>
<span data-ttu-id="09a6b-239">IoT 中樞會對 `tags`、`properties/desired` 和 `properties/reported` 的值 (排除唯讀元素) 強制執行 8 KB 大小的限制。</span><span class="sxs-lookup"><span data-stu-id="09a6b-239">IoT Hub enforces an 8KB size limitation on the values of `tags`, `properties/desired`, and `properties/reported`, excluding read-only elements.</span></span>
<span data-ttu-id="09a6b-240">大小的計算方式是計算所有字元的數量，並排除出現在字串常數之外的 UNICODE 控制字元 (區段 C0 和 C1) 和空格 `' '`。</span><span class="sxs-lookup"><span data-stu-id="09a6b-240">The size is computed by counting all characters excluding UNICODE control characters (segments C0 and C1) and space `' '` when it appears outside of a string constant.</span></span>
<span data-ttu-id="09a6b-241">IoT 中樞會拒絕 (並出現錯誤) 將會讓這些文件的大小增加到超過限制的所有作業。</span><span class="sxs-lookup"><span data-stu-id="09a6b-241">IoT Hub rejects with an error all operations that would increase the size of those documents above the limit.</span></span>

## <a name="device-twin-metadata"></a><span data-ttu-id="09a6b-242">裝置對應項中繼資料</span><span class="sxs-lookup"><span data-stu-id="09a6b-242">Device twin metadata</span></span>
<span data-ttu-id="09a6b-243">IoT 中樞會為裝置對應項所需屬性和報告屬性的每個 JSON 物件保有上次更新的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="09a6b-243">IoT Hub maintains the timestamp of the last update for each JSON object in device twin desired and reported properties.</span></span> <span data-ttu-id="09a6b-244">時間戳記採用 UTC 格式，並以 [ISO8601] 格式 `YYYY-MM-DDTHH:MM:SS.mmmZ` 進行編碼。</span><span class="sxs-lookup"><span data-stu-id="09a6b-244">The timestamps are in UTC and encoded in the [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span></span>
<span data-ttu-id="09a6b-245">例如：</span><span class="sxs-lookup"><span data-stu-id="09a6b-245">For example:</span></span>

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

<span data-ttu-id="09a6b-246">此資訊會保留在每個層級 (而不只是 JSON 結構的分葉)，以保留可移除物件索引鍵的更新。</span><span class="sxs-lookup"><span data-stu-id="09a6b-246">This information is kept at every level (not just the leaves of the JSON structure) to preserve updates that remove object keys.</span></span>

## <a name="optimistic-concurrency"></a><span data-ttu-id="09a6b-247">開放式並行存取</span><span class="sxs-lookup"><span data-stu-id="09a6b-247">Optimistic concurrency</span></span>
<span data-ttu-id="09a6b-248">標籤、所需屬性和報告屬性全都支援開放式並行存取。</span><span class="sxs-lookup"><span data-stu-id="09a6b-248">Tags, desired, and reported properties all support optimistic concurrency.</span></span>
<span data-ttu-id="09a6b-249">依據 [RFC7232]，標籤會有一個 ETag 來表示該標籤的 JSON 表示法。</span><span class="sxs-lookup"><span data-stu-id="09a6b-249">Tags have an ETag, as per [RFC7232], that represents the tag's JSON representation.</span></span> <span data-ttu-id="09a6b-250">您可以從解決方案後端在條件式更新作業中使用 ETag，以確保一致性。</span><span class="sxs-lookup"><span data-stu-id="09a6b-250">You can use ETags in conditional update operations from the solution back end to ensure consistency.</span></span>

<span data-ttu-id="09a6b-251">裝置對應項所需屬性和報告屬性沒有 ETag，但是有一定會遞增的 `$version` 值。</span><span class="sxs-lookup"><span data-stu-id="09a6b-251">Device twin desired and reported properties do not have ETags, but have a `$version` value that is guaranteed to be incremental.</span></span> <span data-ttu-id="09a6b-252">類似於 ETag，更新端可以使用版本強制達到更新的一致性。</span><span class="sxs-lookup"><span data-stu-id="09a6b-252">Similarly to an ETag, the version can be used by the updating party to enforce consistency of updates.</span></span> <span data-ttu-id="09a6b-253">例如，報告屬性的裝置應用程式或所需屬性的解決方案後端。</span><span class="sxs-lookup"><span data-stu-id="09a6b-253">For example, a device app for a reported property or the solution back end for a desired property.</span></span>

<span data-ttu-id="09a6b-254">當觀察端代理程式 (例如，觀察所需屬性的裝置應用程式) 必須協調擷取作業結果與更新通知之間的競爭情況時，版本也相當有用。</span><span class="sxs-lookup"><span data-stu-id="09a6b-254">Versions are also useful when an observing agent (such as the device app observing the desired properties) must reconcile races between the result of a retrieve operation and an update notification.</span></span> <span data-ttu-id="09a6b-255">[裝置重新連線流程][lnk-reconnection]一節會提供詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="09a6b-255">The section [Device reconnection flow][lnk-reconnection] provides more information.</span></span>

## <a name="device-reconnection-flow"></a><span data-ttu-id="09a6b-256">裝置重新連線流程</span><span class="sxs-lookup"><span data-stu-id="09a6b-256">Device reconnection flow</span></span>
<span data-ttu-id="09a6b-257">IoT 中樞不會保留已中斷連線之裝置的所需屬性更新通知。</span><span class="sxs-lookup"><span data-stu-id="09a6b-257">IoT Hub does not preserve desired properties update notifications for disconnected devices.</span></span> <span data-ttu-id="09a6b-258">因此，連線的裝置必須擷取完整的所需屬性文件，並訂閱更新通知。</span><span class="sxs-lookup"><span data-stu-id="09a6b-258">It follows that a device that is connecting must retrieve the full desired properties document, in addition to subscribing for update notifications.</span></span> <span data-ttu-id="09a6b-259">由於更新通知和完整擷取之間可能會有競爭情況，因此必須確保下列流程︰</span><span class="sxs-lookup"><span data-stu-id="09a6b-259">Given the possibility of races between update notifications and full retrieval, the following flow must be ensured:</span></span>

1. <span data-ttu-id="09a6b-260">裝置應用程式連線到 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="09a6b-260">Device app connects to an IoT hub.</span></span>
2. <span data-ttu-id="09a6b-261">裝置應用程式訂閱所需屬性更新通知。</span><span class="sxs-lookup"><span data-stu-id="09a6b-261">Device app subscribes for desired properties update notifications.</span></span>
3. <span data-ttu-id="09a6b-262">裝置應用程式擷取所需屬性的完整文件。</span><span class="sxs-lookup"><span data-stu-id="09a6b-262">Device app retrieves the full document for desired properties.</span></span>

<span data-ttu-id="09a6b-263">裝置應用程式可以忽略 `$version` 小於或等於完整擷取文件版本的所有通知。</span><span class="sxs-lookup"><span data-stu-id="09a6b-263">The device app can ignore all notifications with `$version` less or equal than the version of the full retrieved document.</span></span> <span data-ttu-id="09a6b-264">IoT 中樞保證版本一定會遞增，因此這是可行的方法。</span><span class="sxs-lookup"><span data-stu-id="09a6b-264">This approach is possible because IoT Hub guarantees that versions always increment.</span></span>

> [!NOTE]
> <span data-ttu-id="09a6b-265">[Azure IoT 裝置 SDK][lnk-sdks] 中已實作此邏輯。</span><span class="sxs-lookup"><span data-stu-id="09a6b-265">This logic is already implemented in the [Azure IoT device SDKs][lnk-sdks].</span></span> <span data-ttu-id="09a6b-266">只有當裝置應用程式無法使用任何 Azure IoT 裝置 SDK，因而必須直接為 MQTT 介面編寫程式時，此說明才有用。</span><span class="sxs-lookup"><span data-stu-id="09a6b-266">This description is useful only if the device app cannot use any of Azure IoT device SDKs and must program the MQTT interface directly.</span></span>
> 
> 

## <a name="additional-reference-material"></a><span data-ttu-id="09a6b-267">其他參考資料</span><span class="sxs-lookup"><span data-stu-id="09a6b-267">Additional reference material</span></span>
<span data-ttu-id="09a6b-268">IoT 中樞開發人員指南中的其他參考主題包括︰</span><span class="sxs-lookup"><span data-stu-id="09a6b-268">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="09a6b-269">[IoT 中樞端點][lnk-endpoints]一文說明每個 IoT 中樞針對執行階段和管理作業所公開的各種端點。</span><span class="sxs-lookup"><span data-stu-id="09a6b-269">The [IoT Hub endpoints][lnk-endpoints] article describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="09a6b-270">[節流和配額][lnk-quotas]一文說明適用於 IoT 中樞服務的配額，和使用服務時所預期的節流行為。</span><span class="sxs-lookup"><span data-stu-id="09a6b-270">The [Throttling and quotas][lnk-quotas] article describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="09a6b-271">[Azure IoT 裝置和服務 SDK][lnk-sdks] 一文列出各種語言 SDK，可供您在開發與「IoT 中樞」互動的裝置和服務應用程式時使用。</span><span class="sxs-lookup"><span data-stu-id="09a6b-271">The [Azure IoT device and service SDKs][lnk-sdks] article lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="09a6b-272">[裝置對應項、作業和訊息路由的 IoT 中樞查詢語言][lnk-query]一文說明可用於從 IoT 中樞擷取有關裝置對應項和作業資訊的 IoT 中樞查詢語言。</span><span class="sxs-lookup"><span data-stu-id="09a6b-272">The [IoT Hub query language for device twins, jobs, and message routing][lnk-query] article describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="09a6b-273">[IoT 中樞 MQTT 支援][lnk-devguide-mqtt]一文針對 MQTT 通訊協定提供 IoT 中樞支援的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="09a6b-273">The [IoT Hub MQTT support][lnk-devguide-mqtt] article provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09a6b-274">後續步驟</span><span class="sxs-lookup"><span data-stu-id="09a6b-274">Next steps</span></span>
<span data-ttu-id="09a6b-275">現在您已了解裝置對應項，接下來您可能會對下列 IoT 中樞開發人員指南主題感興趣︰</span><span class="sxs-lookup"><span data-stu-id="09a6b-275">Now you have learned about device twins, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="09a6b-276">[在裝置上叫用直接方法][lnk-methods]</span><span class="sxs-lookup"><span data-stu-id="09a6b-276">[Invoke a direct method on a device][lnk-methods]</span></span>
* <span data-ttu-id="09a6b-277">[排程多個裝置上的作業][lnk-jobs]</span><span class="sxs-lookup"><span data-stu-id="09a6b-277">[Schedule jobs on multiple devices][lnk-jobs]</span></span>

<span data-ttu-id="09a6b-278">如果您想要嘗試本文章所述的概念，您可能會對下列 IoT 中樞教學課程感興趣：</span><span class="sxs-lookup"><span data-stu-id="09a6b-278">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorials:</span></span>

* <span data-ttu-id="09a6b-279">[如何使用裝置對應項][lnk-twin-tutorial]</span><span class="sxs-lookup"><span data-stu-id="09a6b-279">[How to use the device twin][lnk-twin-tutorial]</span></span>
* <span data-ttu-id="09a6b-280">[如何使用裝置對應項屬性][lnk-twin-properties]</span><span class="sxs-lookup"><span data-stu-id="09a6b-280">[How to use device twin properties][lnk-twin-properties]</span></span>

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
