---
title: "遠端監視方案中的裝置資訊中繼資料 | Microsoft Docs"
description: "說明 Azure IoT 預先設定解決方案遠端監視及其架構。"
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
ms.openlocfilehash: f8fd452806a0a0b98cf8e434c9bd55700083a6c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="device-information-metadata-in-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="f1557-103">遠端監視預先設定方案中的裝置資訊中繼資料</span><span class="sxs-lookup"><span data-stu-id="f1557-103">Device information metadata in the remote monitoring preconfigured solution</span></span>

<span data-ttu-id="f1557-104">Azure IoT 套件遠端監視預先設定方案會示範用於管理裝置中繼資料的方法。</span><span class="sxs-lookup"><span data-stu-id="f1557-104">The Azure IoT Suite remote monitoring preconfigured solution demonstrates an approach for managing device metadata.</span></span> <span data-ttu-id="f1557-105">本文將概述此方案為了讓您了解而採用的方法︰</span><span class="sxs-lookup"><span data-stu-id="f1557-105">This article outlines the approach this solution takes to enable you to understand:</span></span>

* <span data-ttu-id="f1557-106">方案會儲存哪些裝置中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f1557-106">What device metadata the solution stores.</span></span>
* <span data-ttu-id="f1557-107">方案如何管理裝置中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f1557-107">How the solution manages the device metadata.</span></span>

## <a name="context"></a><span data-ttu-id="f1557-108">Context</span><span class="sxs-lookup"><span data-stu-id="f1557-108">Context</span></span>

<span data-ttu-id="f1557-109">遠端監視預先設定方案會使用 [Azure IoT 中樞][lnk-iot-hub]，讓您的裝置將資料傳送至雲端。</span><span class="sxs-lookup"><span data-stu-id="f1557-109">The remote monitoring preconfigured solution uses [Azure IoT Hub][lnk-iot-hub] to enable your devices to send data to the cloud.</span></span> <span data-ttu-id="f1557-110">此解決方案會在三個不同位置儲存裝置的相關資訊︰</span><span class="sxs-lookup"><span data-stu-id="f1557-110">The solution stores information about devices in three different locations:</span></span>

| <span data-ttu-id="f1557-111">位置</span><span class="sxs-lookup"><span data-stu-id="f1557-111">Location</span></span> | <span data-ttu-id="f1557-112">儲存的資訊</span><span class="sxs-lookup"><span data-stu-id="f1557-112">Information stored</span></span> | <span data-ttu-id="f1557-113">實作</span><span class="sxs-lookup"><span data-stu-id="f1557-113">Implementation</span></span> |
| -------- | ------------------ | -------------- |
| <span data-ttu-id="f1557-114">身分識別登錄</span><span class="sxs-lookup"><span data-stu-id="f1557-114">Identity registry</span></span> | <span data-ttu-id="f1557-115">裝置識別碼、驗證金鑰和啟用狀態</span><span class="sxs-lookup"><span data-stu-id="f1557-115">Device id, authentication keys, enabled state</span></span> | <span data-ttu-id="f1557-116">內建於 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="f1557-116">Built in to IoT Hub</span></span> |
| <span data-ttu-id="f1557-117">裝置對應項</span><span class="sxs-lookup"><span data-stu-id="f1557-117">Device twins</span></span> | <span data-ttu-id="f1557-118">中繼資料：報告屬性、所需屬性、標記</span><span class="sxs-lookup"><span data-stu-id="f1557-118">Metadata: reported properties, desired properties, tags</span></span> | <span data-ttu-id="f1557-119">內建於 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="f1557-119">Built in to IoT Hub</span></span> |
| <span data-ttu-id="f1557-120">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f1557-120">Cosmos DB</span></span> | <span data-ttu-id="f1557-121">命令和方法歷程記錄</span><span class="sxs-lookup"><span data-stu-id="f1557-121">Command and method history</span></span> | <span data-ttu-id="f1557-122">針對解決方案自訂</span><span class="sxs-lookup"><span data-stu-id="f1557-122">Custom for solution</span></span> |

<span data-ttu-id="f1557-123">IoT 中樞包含可管理 IoT 中樞存取權的[裝置身分識別登錄][lnk-identity-registry]，並使用[裝置對應項][lnk-device-twin]來管理裝置中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f1557-123">IoT Hub includes a [device identity registry][lnk-identity-registry] to manage access to an IoT hub and uses [device twins][lnk-device-twin] to manage device metadata.</span></span> <span data-ttu-id="f1557-124">還有遠端監視解決方案專用*裝置登錄*可儲存命令和方法歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="f1557-124">There is also a remote monitoring solution-specific *device registry* that stores command and method history.</span></span> <span data-ttu-id="f1557-125">遠端監視解決方案會使用 [Cosmos DB][lnk-docdb] 資料庫來實作命令和方法歷程記錄的自訂存放區。</span><span class="sxs-lookup"><span data-stu-id="f1557-125">The remote monitoring solution uses a [Cosmos DB][lnk-docdb] database to implement a custom store for command and method history.</span></span>

> [!NOTE]
> <span data-ttu-id="f1557-126">預先設定的遠端監視解決方案會讓裝置身分識別登錄與 Cosmos DB 資料庫中的資訊保持同步。</span><span class="sxs-lookup"><span data-stu-id="f1557-126">The remote monitoring preconfigured solution keeps the device identity registry in sync with the information in the Cosmos DB database.</span></span> <span data-ttu-id="f1557-127">兩者都使用相同的裝置識別碼來唯一識別連線到您的 IoT 中樞的每個裝置。</span><span class="sxs-lookup"><span data-stu-id="f1557-127">Both use the same device id to uniquely identify each device connected to your IoT hub.</span></span>

## <a name="device-metadata"></a><span data-ttu-id="f1557-128">裝置中繼資料</span><span class="sxs-lookup"><span data-stu-id="f1557-128">Device metadata</span></span>

<span data-ttu-id="f1557-129">IoT 中樞會針對連線至遠端監視解決方案的每個模擬與實體裝置，維護[裝置對應項][lnk-device-twin]。</span><span class="sxs-lookup"><span data-stu-id="f1557-129">IoT Hub maintains a [device twin][lnk-device-twin] for each simulated and physical device connected to a remote monitoring solution.</span></span> <span data-ttu-id="f1557-130">此解決方案會使用裝置對應項來管理與裝置相關聯的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f1557-130">The solution uses device twins to manage the metadata associated with devices.</span></span> <span data-ttu-id="f1557-131">裝置對應項是 IoT 中樞所維護的 JSON 文件，而解決方案會使用 IoT 中樞 API 來與裝置對應項互動。</span><span class="sxs-lookup"><span data-stu-id="f1557-131">A device twin is a JSON document maintained by IoT Hub, and the solution uses the IoT Hub API to interact with device twins.</span></span>

<span data-ttu-id="f1557-132">裝置對應項可儲存三種中繼資料︰</span><span class="sxs-lookup"><span data-stu-id="f1557-132">A device twin stores three types of metadata:</span></span>

- <span data-ttu-id="f1557-133">「報告屬性」是由裝置傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f1557-133">*Reported properties* are sent to an IoT hub by a device.</span></span> <span data-ttu-id="f1557-134">在遠端監視解決方案中，模擬裝置會在啟動時傳送報告屬性，以回應**變更裝置狀態**命令和方法。</span><span class="sxs-lookup"><span data-stu-id="f1557-134">In the remote monitoring solution, simulated devices send reported properties at start-up and in response to **Change device state** commands and methods.</span></span> <span data-ttu-id="f1557-135">您可以在解決方案入口網站的 [裝置清單] 和 [裝置詳細資料] 中檢視報告屬性。</span><span class="sxs-lookup"><span data-stu-id="f1557-135">You can view reported properties in the **Device list** and **Device details** in the solution portal.</span></span> <span data-ttu-id="f1557-136">報告屬性是唯讀的。</span><span class="sxs-lookup"><span data-stu-id="f1557-136">Reported properties are read only.</span></span>
- <span data-ttu-id="f1557-137">「所需屬性」是由裝置從 IoT 中樞擷取。</span><span class="sxs-lookup"><span data-stu-id="f1557-137">*Desired properties* are retrieved from the IoT hub by devices.</span></span> <span data-ttu-id="f1557-138">在裝置上進行任何必要的組態變更是裝置的責任。</span><span class="sxs-lookup"><span data-stu-id="f1557-138">It is the responsibility of the device to make any necessary configuration change on the device.</span></span> <span data-ttu-id="f1557-139">以報告屬性形式向中樞回報變更也是裝置的責任。</span><span class="sxs-lookup"><span data-stu-id="f1557-139">It is also the responsibility of the device to report the change back to the hub as a reported property.</span></span> <span data-ttu-id="f1557-140">您可以透過解決方案入口網站設定所需屬性值。</span><span class="sxs-lookup"><span data-stu-id="f1557-140">You can set a desired property value through the solution portal.</span></span>
- <span data-ttu-id="f1557-141">*標記*只存在於裝置對應項中，永遠不會與裝置同步處理。</span><span class="sxs-lookup"><span data-stu-id="f1557-141">*Tags* only exist in the device twin and are never synchronized with a device.</span></span> <span data-ttu-id="f1557-142">您可以在解決方案入口網站中設定標記值，並且在篩選裝置清單時加以使用。</span><span class="sxs-lookup"><span data-stu-id="f1557-142">You can set tag values in the solution portal and use them when you filter the list of devices.</span></span> <span data-ttu-id="f1557-143">解決方案也會使用標記來識別在解決方案入口網站中要針對裝置顯示的圖示。</span><span class="sxs-lookup"><span data-stu-id="f1557-143">The solution also uses a tag to identify the icon to display for a device in the solution portal.</span></span>

<span data-ttu-id="f1557-144">模擬裝置的範例報告屬性包括製造商、型號、緯度和經度。</span><span class="sxs-lookup"><span data-stu-id="f1557-144">Example reported properties from the simulated devices include manufacturer, model number, latitude, and longitude.</span></span> <span data-ttu-id="f1557-145">模擬裝置也會以報告屬性形式傳回支援的方法清單。</span><span class="sxs-lookup"><span data-stu-id="f1557-145">Simulated devices also return the list of supported methods as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="f1557-146">模擬裝置程式碼只會使用 **Desired.Config.TemperatureMeanValue** 和 **Desired.Config.TelemetryInterval** 所需屬性來更新送回 IoT 中樞的報告屬性。</span><span class="sxs-lookup"><span data-stu-id="f1557-146">The simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties sent back to IoT Hub.</span></span> <span data-ttu-id="f1557-147">所有其他所需屬性變更要求都會被忽略。</span><span class="sxs-lookup"><span data-stu-id="f1557-147">All other desired property change requests are ignored.</span></span>

<span data-ttu-id="f1557-148">儲存在裝置登錄 Cosmos DB 資料庫中的裝置資訊中繼資料 JSON 文件具有下列結構︰</span><span class="sxs-lookup"><span data-stu-id="f1557-148">A device information metadata JSON document stored in the device registry Cosmos DB database has the following structure:</span></span>

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
> <span data-ttu-id="f1557-149">裝置訊息也可包含中繼資料，以描述裝置傳送給 IoT 中樞的遙測。</span><span class="sxs-lookup"><span data-stu-id="f1557-149">Device information can also include metadata to describe the telemetry the device sends to IoT Hub.</span></span> <span data-ttu-id="f1557-150">遠端監視方案會使用此遙測中繼資料，來自訂儀表板顯示[動態遙測][lnk-dynamic-telemetry]的方式。</span><span class="sxs-lookup"><span data-stu-id="f1557-150">The remote monitoring solution uses this telemetry metadata to customize how the dashboard displays [dynamic telemetry][lnk-dynamic-telemetry].</span></span>

## <a name="lifecycle"></a><span data-ttu-id="f1557-151">生命週期</span><span class="sxs-lookup"><span data-stu-id="f1557-151">Lifecycle</span></span>

<span data-ttu-id="f1557-152">當您第一次在解決方案入口網站中建立裝置時，解決方案會在 Cosmos DB 資料庫中建立一個項目，以儲存命令和方法歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="f1557-152">When you first create a device in the solution portal, the solution creates an entry in the Cosmos DB database to store command and method history.</span></span> <span data-ttu-id="f1557-153">此時，方案也會在裝置身分識別登錄中為裝置建立一個項目，以產生裝置用來向「IoT 中樞」進行驗證的金鑰。</span><span class="sxs-lookup"><span data-stu-id="f1557-153">At this point, the solution also creates an entry for the device in the device identity registry, which generates the keys the device uses to authenticate with IoT Hub.</span></span> <span data-ttu-id="f1557-154">它也會建立裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="f1557-154">It also creates a device twin.</span></span>

<span data-ttu-id="f1557-155">當裝置第一次連線至解決方案時，它會傳送報告屬性和裝置資訊訊息。</span><span class="sxs-lookup"><span data-stu-id="f1557-155">When a device first connects to the solution, it sends reported properties and a device information message.</span></span> <span data-ttu-id="f1557-156">報告屬性值會自動儲存在裝置對應項中。</span><span class="sxs-lookup"><span data-stu-id="f1557-156">The reported property values are automatically saved in the device twin.</span></span> <span data-ttu-id="f1557-157">報告屬性包括裝置製造商、型號、序號及支援的方法清單。</span><span class="sxs-lookup"><span data-stu-id="f1557-157">The reported properties include the device manufacturer, model number, serial number, and a list of supported methods.</span></span> <span data-ttu-id="f1557-158">裝置資訊訊息包含裝置支援的命令清單，其中包括任何命令參數的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f1557-158">The device information message includes the list of the commands the device supports including information about any command parameters.</span></span> <span data-ttu-id="f1557-159">當解決方案收到此訊息時，它會更新 Cosmos DB 資料庫中的裝置資訊。</span><span class="sxs-lookup"><span data-stu-id="f1557-159">When the solution receives this message, it updates the device information in the Cosmos DB database.</span></span>

### <a name="view-and-edit-device-information-in-the-solution-portal"></a><span data-ttu-id="f1557-160">在方案入口網站中檢視和編輯裝置資訊</span><span class="sxs-lookup"><span data-stu-id="f1557-160">View and edit device information in the solution portal</span></span>

<span data-ttu-id="f1557-161">解決方案入口網站中的裝置清單預設會將下列裝置屬性顯示為資料行︰[狀態]、[裝置識別碼]、[製造商]、[型號編號]、[序號]、[韌體]、[平台]、[處理器] 和 [已安裝的 RAM]。</span><span class="sxs-lookup"><span data-stu-id="f1557-161">The device list in the solution portal displays the following device properties as columns by default: **Status**, **DeviceId**, **Manufacturer**, **Model Number**, **Serial Number**, **Firmware**, **Platform**, **Processor**, and **Installed RAM**.</span></span> <span data-ttu-id="f1557-162">您可以按一下 [資料行編輯器] 來自訂資料行。</span><span class="sxs-lookup"><span data-stu-id="f1557-162">You can customize the columns by clicking **Column editor**.</span></span> <span data-ttu-id="f1557-163">裝置屬性 [緯度] 和 [經度] 會支配儀表板上「Bing 地圖」中的位置。</span><span class="sxs-lookup"><span data-stu-id="f1557-163">The device properties **Latitude** and **Longitude** drive the location in the Bing Map on the dashboard.</span></span>

![裝置清單中的資料行編輯器][img-device-list]

<span data-ttu-id="f1557-165">在解決方案入口網站的 [裝置詳細資料] 窗格中，您可以編輯所需屬性和標記 (報告屬性是唯讀)。</span><span class="sxs-lookup"><span data-stu-id="f1557-165">In the **Device Details** pane in the solution portal, you can edit desired properties and tags (reported properties are read only).</span></span>

![裝置詳細資料窗格][img-device-edit]

<span data-ttu-id="f1557-167">您可以使用方案入口網站，從您的方案中移除裝置。</span><span class="sxs-lookup"><span data-stu-id="f1557-167">You can use the solution portal to remove a device from your solution.</span></span> <span data-ttu-id="f1557-168">當您移除裝置時，解決方案會從身分識別登錄中移除此裝置項目，然後刪除裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="f1557-168">When you remove a device, the solution removes the device entry from identity registry and then deletes the device twin.</span></span> <span data-ttu-id="f1557-169">解決方案也會從 Cosmos DB 資料庫中移除裝置相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f1557-169">The solution also removes information related to the device from the Cosmos DB database.</span></span> <span data-ttu-id="f1557-170">您必須先停用裝置，才可以將它移除。</span><span class="sxs-lookup"><span data-stu-id="f1557-170">Before you can remove a device, you must disable it.</span></span>

![移除裝置][img-device-remove]

## <a name="device-information-message-processing"></a><span data-ttu-id="f1557-172">裝置資訊訊息處理</span><span class="sxs-lookup"><span data-stu-id="f1557-172">Device information message processing</span></span>

<span data-ttu-id="f1557-173">裝置所傳送的裝置資訊訊息與遙測訊息不同。</span><span class="sxs-lookup"><span data-stu-id="f1557-173">Device information messages sent by a device are distinct from telemetry messages.</span></span> <span data-ttu-id="f1557-174">裝置資訊訊息包含裝置可以回應的命令以及任何命令歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="f1557-174">Device information messages include the commands a device can respond to, and any command history.</span></span> <span data-ttu-id="f1557-175">IoT 中樞本身不知道裝置資訊訊息中內含的中繼資料，它會以處理任何裝置對雲端訊息的相同方式處理訊息。</span><span class="sxs-lookup"><span data-stu-id="f1557-175">IoT Hub itself has no knowledge of the metadata contained in a device information message and processes the message in the same way it processes any device-to-cloud message.</span></span> <span data-ttu-id="f1557-176">在遠端監視方案中，[Azure 串流分析][lnk-stream-analytics] (ASA) 作業會從「IoT 中樞」讀取訊息。</span><span class="sxs-lookup"><span data-stu-id="f1557-176">In the remote monitoring solution, an [Azure Stream Analytics][lnk-stream-analytics] (ASA) job reads the messages from IoT Hub.</span></span> <span data-ttu-id="f1557-177">**DeviceInfo** 串流分析作業會篩選包含 **"ObjectType":"DeviceInfo"** 的訊息，並將這些訊息轉送至在 Web 作業中執行的 **EventProcessorHost** 主機執行個體。</span><span class="sxs-lookup"><span data-stu-id="f1557-177">The **DeviceInfo** stream analytics job filters for messages that contain **"ObjectType": "DeviceInfo"** and forwards them to the **EventProcessorHost** host instance that runs in a web job.</span></span> <span data-ttu-id="f1557-178">**EventProcessorHost** 執行個體中的邏輯會使用裝置識別碼，來尋找特定裝置的 Cosmos DB 記錄並更新該記錄。</span><span class="sxs-lookup"><span data-stu-id="f1557-178">Logic in the **EventProcessorHost** instance uses the device id to find the Cosmos DB record for the specific device and update the record.</span></span>

> [!NOTE]
> <span data-ttu-id="f1557-179">裝置資訊訊息是標準的裝置對雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="f1557-179">A device information message is a standard device-to-cloud message.</span></span> <span data-ttu-id="f1557-180">方案會使用 ASA 查詢，以區分裝置資訊訊息與遙測訊息。</span><span class="sxs-lookup"><span data-stu-id="f1557-180">The solution distinguishes between device information messages and telemetry messages by using ASA queries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1557-181">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f1557-181">Next steps</span></span>

<span data-ttu-id="f1557-182">現在您已完成了解如何自訂預先設定的解決方案，您可以瀏覽一些其他功能和預先設定的 IoT 套件解決方案的功能︰</span><span class="sxs-lookup"><span data-stu-id="f1557-182">Now you've finished learning how you can customize the preconfigured solutions, you can explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="f1557-183">[預先設定的預防性維護解決方案概觀][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="f1557-183">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* <span data-ttu-id="f1557-184">[IoT 套件的常見問題集][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="f1557-184">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="f1557-185">[從頭建立 IoT 安全性][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="f1557-185">[IoT security from the ground up][lnk-security-groundup]</span></span>

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
