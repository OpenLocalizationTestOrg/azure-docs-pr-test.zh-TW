---
title: "aaaDevice 資訊的中繼資料中 hello 遠端監視解決方案 |Microsoft 文件"
description: "Hello 預先設定的 Azure IoT 解決方案遠端監視和其結構描述。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1b334769-103b-4eb0-a293-184f3d1ba9a3
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 8387b98b8b2ae4934b0c900bc4df37dc17337c60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="device-information-metadata-in-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="d3582-103">裝置資訊的中繼資料中 hello 遠端監視預先設定的解決方案</span><span class="sxs-lookup"><span data-stu-id="d3582-103">Device information metadata in hello remote monitoring preconfigured solution</span></span>

<span data-ttu-id="d3582-104">hello Azure IoT 套件遠端監視預先設定的解決方案示範管理裝置的中繼資料的方法。</span><span class="sxs-lookup"><span data-stu-id="d3582-104">hello Azure IoT Suite remote monitoring preconfigured solution demonstrates an approach for managing device metadata.</span></span> <span data-ttu-id="d3582-105">本文將概述 hello 方法此解決方案會 tooenable 您 toounderstand:</span><span class="sxs-lookup"><span data-stu-id="d3582-105">This article outlines hello approach this solution takes tooenable you toounderstand:</span></span>

* <span data-ttu-id="d3582-106">會儲存哪些裝置中繼資料 hello 解決方案。</span><span class="sxs-lookup"><span data-stu-id="d3582-106">What device metadata hello solution stores.</span></span>
* <span data-ttu-id="d3582-107">Hello 方案管理 hello 裝置中繼資料的方式。</span><span class="sxs-lookup"><span data-stu-id="d3582-107">How hello solution manages hello device metadata.</span></span>

## <a name="context"></a><span data-ttu-id="d3582-108">Context</span><span class="sxs-lookup"><span data-stu-id="d3582-108">Context</span></span>

<span data-ttu-id="d3582-109">hello 遠端監視預先設定的解決方案會使用[Azure IoT 中樞][ lnk-iot-hub] tooenable 您裝置 toosend 資料 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="d3582-109">hello remote monitoring preconfigured solution uses [Azure IoT Hub][lnk-iot-hub] tooenable your devices toosend data toohello cloud.</span></span> <span data-ttu-id="d3582-110">hello 方案會在三個不同的位置儲存裝置的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="d3582-110">hello solution stores information about devices in three different locations:</span></span>

| <span data-ttu-id="d3582-111">位置</span><span class="sxs-lookup"><span data-stu-id="d3582-111">Location</span></span> | <span data-ttu-id="d3582-112">儲存的資訊</span><span class="sxs-lookup"><span data-stu-id="d3582-112">Information stored</span></span> | <span data-ttu-id="d3582-113">實作</span><span class="sxs-lookup"><span data-stu-id="d3582-113">Implementation</span></span> |
| -------- | ------------------ | -------------- |
| <span data-ttu-id="d3582-114">身分識別登錄</span><span class="sxs-lookup"><span data-stu-id="d3582-114">Identity registry</span></span> | <span data-ttu-id="d3582-115">裝置識別碼、驗證金鑰和啟用狀態</span><span class="sxs-lookup"><span data-stu-id="d3582-115">Device id, authentication keys, enabled state</span></span> | <span data-ttu-id="d3582-116">內建的 tooIoT 中樞</span><span class="sxs-lookup"><span data-stu-id="d3582-116">Built in tooIoT Hub</span></span> |
| <span data-ttu-id="d3582-117">裝置對應項</span><span class="sxs-lookup"><span data-stu-id="d3582-117">Device twins</span></span> | <span data-ttu-id="d3582-118">中繼資料：報告屬性、所需屬性、標記</span><span class="sxs-lookup"><span data-stu-id="d3582-118">Metadata: reported properties, desired properties, tags</span></span> | <span data-ttu-id="d3582-119">內建的 tooIoT 中樞</span><span class="sxs-lookup"><span data-stu-id="d3582-119">Built in tooIoT Hub</span></span> |
| <span data-ttu-id="d3582-120">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d3582-120">Cosmos DB</span></span> | <span data-ttu-id="d3582-121">命令和方法歷程記錄</span><span class="sxs-lookup"><span data-stu-id="d3582-121">Command and method history</span></span> | <span data-ttu-id="d3582-122">針對解決方案自訂</span><span class="sxs-lookup"><span data-stu-id="d3582-122">Custom for solution</span></span> |

<span data-ttu-id="d3582-123">IoT 中樞包含[裝置身分登錄][ lnk-identity-registry] toomanage 存取 tooan IoT 中樞，並使用[裝置雙][ lnk-device-twin] toomanage 裝置中繼資料.</span><span class="sxs-lookup"><span data-stu-id="d3582-123">IoT Hub includes a [device identity registry][lnk-identity-registry] toomanage access tooan IoT hub and uses [device twins][lnk-device-twin] toomanage device metadata.</span></span> <span data-ttu-id="d3582-124">還有遠端監視解決方案專用*裝置登錄*可儲存命令和方法歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="d3582-124">There is also a remote monitoring solution-specific *device registry* that stores command and method history.</span></span> <span data-ttu-id="d3582-125">遠端監視解決方案使用 hello [Cosmos DB] [ lnk-docdb]資料庫 tooimplement 命令和方法的歷程記錄的自訂存放區。</span><span class="sxs-lookup"><span data-stu-id="d3582-125">hello remote monitoring solution uses a [Cosmos DB][lnk-docdb] database tooimplement a custom store for command and method history.</span></span>

> [!NOTE]
> <span data-ttu-id="d3582-126">hello 遠端監視預先設定的解決方案會保留 hello 裝置身分登錄與 hello 資訊同步 hello Cosmos DB 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="d3582-126">hello remote monitoring preconfigured solution keeps hello device identity registry in sync with hello information in hello Cosmos DB database.</span></span> <span data-ttu-id="d3582-127">兩者都使用相同的裝置識別碼 toouniquely 識別的 hello 連接 tooyour IoT 中樞的每個裝置。</span><span class="sxs-lookup"><span data-stu-id="d3582-127">Both use hello same device id toouniquely identify each device connected tooyour IoT hub.</span></span>

## <a name="device-metadata"></a><span data-ttu-id="d3582-128">裝置中繼資料</span><span class="sxs-lookup"><span data-stu-id="d3582-128">Device metadata</span></span>

<span data-ttu-id="d3582-129">IoT 中樞維護[裝置兩個][ lnk-device-twin]針對每個模擬與實體裝置連線 tooa 遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="d3582-129">IoT Hub maintains a [device twin][lnk-device-twin] for each simulated and physical device connected tooa remote monitoring solution.</span></span> <span data-ttu-id="d3582-130">hello 解決方案會使用裝置雙 toomanage hello 中繼資料與裝置相關聯。</span><span class="sxs-lookup"><span data-stu-id="d3582-130">hello solution uses device twins toomanage hello metadata associated with devices.</span></span> <span data-ttu-id="d3582-131">裝置的兩個是由 IoT 中樞維護的 JSON 文件和 hello 方案會使用裝置雙 hello IoT 中樞 API toointeract。</span><span class="sxs-lookup"><span data-stu-id="d3582-131">A device twin is a JSON document maintained by IoT Hub, and hello solution uses hello IoT Hub API toointeract with device twins.</span></span>

<span data-ttu-id="d3582-132">裝置對應項可儲存三種中繼資料︰</span><span class="sxs-lookup"><span data-stu-id="d3582-132">A device twin stores three types of metadata:</span></span>

- <span data-ttu-id="d3582-133">*報告內容*tooan IoT 中樞傳送的裝置。</span><span class="sxs-lookup"><span data-stu-id="d3582-133">*Reported properties* are sent tooan IoT hub by a device.</span></span> <span data-ttu-id="d3582-134">Hello 遠端監視解決方案，在模擬的裝置傳送報告的內容在啟動時，以回應太**變更裝置狀態**命令和方法。</span><span class="sxs-lookup"><span data-stu-id="d3582-134">In hello remote monitoring solution, simulated devices send reported properties at start-up and in response too**Change device state** commands and methods.</span></span> <span data-ttu-id="d3582-135">您可以檢視報告的內容中 hello**裝置清單**和**裝置詳細資料**hello 方案入口網站中。</span><span class="sxs-lookup"><span data-stu-id="d3582-135">You can view reported properties in hello **Device list** and **Device details** in hello solution portal.</span></span> <span data-ttu-id="d3582-136">報告屬性是唯讀的。</span><span class="sxs-lookup"><span data-stu-id="d3582-136">Reported properties are read only.</span></span>
- <span data-ttu-id="d3582-137">*所需屬性*取自裝置 hello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="d3582-137">*Desired properties* are retrieved from hello IoT hub by devices.</span></span> <span data-ttu-id="d3582-138">它負責 hello hello 裝置 toomake hello 裝置的任何必要的組態變更。</span><span class="sxs-lookup"><span data-stu-id="d3582-138">It is hello responsibility of hello device toomake any necessary configuration change on hello device.</span></span> <span data-ttu-id="d3582-139">它也是做為報告屬性 hello 裝置 tooreport hello 變更後 toohello 中樞 hello 責任。</span><span class="sxs-lookup"><span data-stu-id="d3582-139">It is also hello responsibility of hello device tooreport hello change back toohello hub as a reported property.</span></span> <span data-ttu-id="d3582-140">您可以設定透過 hello 方案入口網站所需的屬性值。</span><span class="sxs-lookup"><span data-stu-id="d3582-140">You can set a desired property value through hello solution portal.</span></span>
- <span data-ttu-id="d3582-141">*標記*只存在於 hello 裝置兩個，並永遠不會與裝置同步處理。</span><span class="sxs-lookup"><span data-stu-id="d3582-141">*Tags* only exist in hello device twin and are never synchronized with a device.</span></span> <span data-ttu-id="d3582-142">您可以在 hello 方案入口網站設定標記值，並使用它們，當您篩選 hello 的裝置清單。</span><span class="sxs-lookup"><span data-stu-id="d3582-142">You can set tag values in hello solution portal and use them when you filter hello list of devices.</span></span> <span data-ttu-id="d3582-143">hello 解決方案也會使用標記 tooidentify hello 圖示 toodisplay hello 方案入口網站中的裝置。</span><span class="sxs-lookup"><span data-stu-id="d3582-143">hello solution also uses a tag tooidentify hello icon toodisplay for a device in hello solution portal.</span></span>

<span data-ttu-id="d3582-144">範例會報告從 hello 模擬裝置的屬性包括製造商、 型號、 緯度與經度。</span><span class="sxs-lookup"><span data-stu-id="d3582-144">Example reported properties from hello simulated devices include manufacturer, model number, latitude, and longitude.</span></span> <span data-ttu-id="d3582-145">模擬的裝置也會傳回 hello 清單支援的方法做為報告的屬性。</span><span class="sxs-lookup"><span data-stu-id="d3582-145">Simulated devices also return hello list of supported methods as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="d3582-146">hello 模擬的裝置的程式碼只會使用 hello **Desired.Config.TemperatureMeanValue**和**Desired.Config.TelemetryInterval**需的屬性 tooupdate hello 報告傳送回屬性tooIoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="d3582-146">hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties sent back tooIoT Hub.</span></span> <span data-ttu-id="d3582-147">所有其他所需屬性變更要求都會被忽略。</span><span class="sxs-lookup"><span data-stu-id="d3582-147">All other desired property change requests are ignored.</span></span>

<span data-ttu-id="d3582-148">裝置資訊的中繼資料 JSON 文件儲存在 hello 裝置登錄 Cosmos DB 資料庫具有下列結構的 hello:</span><span class="sxs-lookup"><span data-stu-id="d3582-148">A device information metadata JSON document stored in hello device registry Cosmos DB database has hello following structure:</span></span>

```json
{
  "DeviceProperties": {
    "DeviceID": "deviceid1",
    "HubEnabledState": null,
    "CreatedTime": "2016-04-25T23:54:01.313802Z",
    "DeviceState": "normal",
    "UpdatedTime": null
    },
  "SystemProperties": {
    "ICCID": null
  },
  "Commands": [],
  "CommandHistory": [],
  "IsSimulatedDevice": false,
  "id": "fe81a81c-bcbc-4970-81f4-7f12f2d8bda8"
}
```

> [!NOTE]
> <span data-ttu-id="d3582-149">裝置資訊也可以包含中繼資料 toodescribe hello 遙測 hello 裝置傳送 tooIoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="d3582-149">Device information can also include metadata toodescribe hello telemetry hello device sends tooIoT Hub.</span></span> <span data-ttu-id="d3582-150">hello 遠端監視解決方案會使用這個 hello 儀表板的顯示方式的遙測中繼資料 toocustomize[動態遙測][lnk-dynamic-telemetry]。</span><span class="sxs-lookup"><span data-stu-id="d3582-150">hello remote monitoring solution uses this telemetry metadata toocustomize how hello dashboard displays [dynamic telemetry][lnk-dynamic-telemetry].</span></span>

## <a name="lifecycle"></a><span data-ttu-id="d3582-151">生命週期</span><span class="sxs-lookup"><span data-stu-id="d3582-151">Lifecycle</span></span>

<span data-ttu-id="d3582-152">當您第一次可以建立裝置 hello 方案入口網站中時，hello 方案建立 hello Cosmos DB 資料庫 toostore 命令中的項目和方法歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="d3582-152">When you first create a device in hello solution portal, hello solution creates an entry in hello Cosmos DB database toostore command and method history.</span></span> <span data-ttu-id="d3582-153">此時，hello 解決方案也會建立 hello 裝置項目在 hello 裝置身分識別登錄中，會產生 hello 金鑰 hello 裝置使用 tooauthenticate 與 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="d3582-153">At this point, hello solution also creates an entry for hello device in hello device identity registry, which generates hello keys hello device uses tooauthenticate with IoT Hub.</span></span> <span data-ttu-id="d3582-154">它也會建立裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="d3582-154">It also creates a device twin.</span></span>

<span data-ttu-id="d3582-155">當裝置第一次連接 toohello 方案時，它會傳送報告的屬性和裝置資訊訊息。</span><span class="sxs-lookup"><span data-stu-id="d3582-155">When a device first connects toohello solution, it sends reported properties and a device information message.</span></span> <span data-ttu-id="d3582-156">hello 報告屬性值會自動儲存在 hello 裝置兩個。</span><span class="sxs-lookup"><span data-stu-id="d3582-156">hello reported property values are automatically saved in hello device twin.</span></span> <span data-ttu-id="d3582-157">hello 報告屬性包括 hello 裝置製造商、 型號、 序號和支援的方法清單。</span><span class="sxs-lookup"><span data-stu-id="d3582-157">hello reported properties include hello device manufacturer, model number, serial number, and a list of supported methods.</span></span> <span data-ttu-id="d3582-158">hello 裝置資訊訊息包含 hello hello 裝置支援包括任何命令參數的相關資訊的 hello 命令清單。</span><span class="sxs-lookup"><span data-stu-id="d3582-158">hello device information message includes hello list of hello commands hello device supports including information about any command parameters.</span></span> <span data-ttu-id="d3582-159">Hello 方案收到此訊息時，它會更新 hello hello Cosmos DB 資料庫中的裝置資訊。</span><span class="sxs-lookup"><span data-stu-id="d3582-159">When hello solution receives this message, it updates hello device information in hello Cosmos DB database.</span></span>

### <a name="view-and-edit-device-information-in-hello-solution-portal"></a><span data-ttu-id="d3582-160">檢視和編輯 hello 方案入口網站中的裝置資訊</span><span class="sxs-lookup"><span data-stu-id="d3582-160">View and edit device information in hello solution portal</span></span>

<span data-ttu-id="d3582-161">hello hello 方案入口網站中的 [裝置] 清單會顯示下列資料行的裝置屬性，預設的 hello:**狀態**， **DeviceId**，**製造商**， **型號**，**序號**，**韌體**，**平台**，**處理器**，和**安裝 RAM**。</span><span class="sxs-lookup"><span data-stu-id="d3582-161">hello device list in hello solution portal displays hello following device properties as columns by default: **Status**, **DeviceId**, **Manufacturer**, **Model Number**, **Serial Number**, **Firmware**, **Platform**, **Processor**, and **Installed RAM**.</span></span> <span data-ttu-id="d3582-162">您可以按一下自訂 hello 行**資料行編輯器**。</span><span class="sxs-lookup"><span data-stu-id="d3582-162">You can customize hello columns by clicking **Column editor**.</span></span> <span data-ttu-id="d3582-163">hello 裝置屬性**緯度**和**經度**hello 儀表板上的磁碟機 hello Bing 地圖中的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="d3582-163">hello device properties **Latitude** and **Longitude** drive hello location in hello Bing Map on hello dashboard.</span></span>

![裝置清單中的資料行編輯器][img-device-list]

<span data-ttu-id="d3582-165">在 hello**裝置詳細資料**窗格在 hello 方案入口網站中，您可以編輯所需的屬性和標記 （報告屬性唯讀）。</span><span class="sxs-lookup"><span data-stu-id="d3582-165">In hello **Device Details** pane in hello solution portal, you can edit desired properties and tags (reported properties are read only).</span></span>

![裝置詳細資料窗格][img-device-edit]

<span data-ttu-id="d3582-167">您可以從您的方案使用 hello 方案入口網站 tooremove 裝置。</span><span class="sxs-lookup"><span data-stu-id="d3582-167">You can use hello solution portal tooremove a device from your solution.</span></span> <span data-ttu-id="d3582-168">當您移除裝置時，hello 方案會從身分識別登錄移除 hello 裝置項目，然後再刪除 hello 裝置兩個。</span><span class="sxs-lookup"><span data-stu-id="d3582-168">When you remove a device, hello solution removes hello device entry from identity registry and then deletes hello device twin.</span></span> <span data-ttu-id="d3582-169">hello 解決方案也會從 hello Cosmos DB 資料庫移除資訊相關的 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="d3582-169">hello solution also removes information related toohello device from hello Cosmos DB database.</span></span> <span data-ttu-id="d3582-170">您必須先停用裝置，才可以將它移除。</span><span class="sxs-lookup"><span data-stu-id="d3582-170">Before you can remove a device, you must disable it.</span></span>

![移除裝置][img-device-remove]

## <a name="device-information-message-processing"></a><span data-ttu-id="d3582-172">裝置資訊訊息處理</span><span class="sxs-lookup"><span data-stu-id="d3582-172">Device information message processing</span></span>

<span data-ttu-id="d3582-173">裝置所傳送的裝置資訊訊息與遙測訊息不同。</span><span class="sxs-lookup"><span data-stu-id="d3582-173">Device information messages sent by a device are distinct from telemetry messages.</span></span> <span data-ttu-id="d3582-174">裝置資訊訊息包括裝置可回應 hello 命令和任何命令歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="d3582-174">Device information messages include hello commands a device can respond to, and any command history.</span></span> <span data-ttu-id="d3582-175">IoT 中樞本身並不了解包含裝置資訊訊息中的 hello 中繼資料和處理序 hello 中 hello 訊息處理的任何裝置到雲端訊息的方式相同。</span><span class="sxs-lookup"><span data-stu-id="d3582-175">IoT Hub itself has no knowledge of hello metadata contained in a device information message and processes hello message in hello same way it processes any device-to-cloud message.</span></span> <span data-ttu-id="d3582-176">在遠端監視解決方案，hello [Azure Stream Analytics] [ lnk-stream-analytics] (ASA) 作業會從 IoT 中樞讀取 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="d3582-176">In hello remote monitoring solution, an [Azure Stream Analytics][lnk-stream-analytics] (ASA) job reads hello messages from IoT Hub.</span></span> <span data-ttu-id="d3582-177">hello **DeviceInfo** stream analytics 工作包含的訊息篩選條件**"ObjectType":"DeviceInfo"**並將它們轉送 toohello **EventProcessorHost**主機web 工作中執行的執行個體。</span><span class="sxs-lookup"><span data-stu-id="d3582-177">hello **DeviceInfo** stream analytics job filters for messages that contain **"ObjectType": "DeviceInfo"** and forwards them toohello **EventProcessorHost** host instance that runs in a web job.</span></span> <span data-ttu-id="d3582-178">Hello 中的邏輯**EventProcessorHost**執行個體會使用 hello 特定裝置與更新 hello 記錄 hello 裝置識別碼 toofind hello Cosmos DB 記錄。</span><span class="sxs-lookup"><span data-stu-id="d3582-178">Logic in hello **EventProcessorHost** instance uses hello device id toofind hello Cosmos DB record for hello specific device and update hello record.</span></span>

> [!NOTE]
> <span data-ttu-id="d3582-179">裝置資訊訊息是標準的裝置對雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="d3582-179">A device information message is a standard device-to-cloud message.</span></span> <span data-ttu-id="d3582-180">hello 方案區分裝置的資訊訊息和遙測訊息使用 ASA 查詢。</span><span class="sxs-lookup"><span data-stu-id="d3582-180">hello solution distinguishes between device information messages and telemetry messages by using ASA queries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3582-181">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d3582-181">Next steps</span></span>

<span data-ttu-id="d3582-182">現在您已完成學習如何自訂 hello 預先設定的解決方案，您可以瀏覽 hello 的某些其他特性和功能 hello IoT 套件預先設定的解決方案：</span><span class="sxs-lookup"><span data-stu-id="d3582-182">Now you've finished learning how you can customize hello preconfigured solutions, you can explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="d3582-183">[預先設定的預防性維護解決方案概觀][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="d3582-183">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* <span data-ttu-id="d3582-184">[IoT 套件的常見問題集][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="d3582-184">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="d3582-185">[從 hello 接地 IoT 安全性][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="d3582-185">[IoT security from hello ground up][lnk-security-groundup]</span></span>

<!-- Images and links -->
[img-device-list]: media/iot-suite-remote-monitoring-device-info/image1.png
[img-device-edit]: media/iot-suite-remote-monitoring-device-info/image2.png
[img-device-remove]: media/iot-suite-remote-monitoring-device-info/image3.png

[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-docdb]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-stream-analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
