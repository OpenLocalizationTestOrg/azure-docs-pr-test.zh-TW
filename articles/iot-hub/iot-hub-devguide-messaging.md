---
title: "aaaUnderstand Azure IoT 中樞傳訊 |Microsoft 文件"
description: "開發人員指南 - IoT 中樞的裝置到雲端及雲端到裝置傳訊。 其中包括訊息格式和支援之通訊協定的相關資訊。"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: a610741e23e243f392f1c042f9ab4a00d42f734f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a><span data-ttu-id="821ea-104">IoT 中樞的裝置到雲端及雲端到裝置傳訊</span><span class="sxs-lookup"><span data-stu-id="821ea-104">Device-to-cloud and cloud-to-device messaging with IoT Hub</span></span>

<span data-ttu-id="821ea-105">使用 IoT 中樞傳訊 toocommunicate 與依裝置：</span><span class="sxs-lookup"><span data-stu-id="821ea-105">Use IoT Hub messaging toocommunicate with your devices by:</span></span>

* <span data-ttu-id="821ea-106">傳送[裝置到雲端][ lnk-d2c]訊息從您的裝置 tooyour 方案後端。</span><span class="sxs-lookup"><span data-stu-id="821ea-106">Sending [device-to-cloud][lnk-d2c] messages from your devices tooyour solution back end.</span></span>
* <span data-ttu-id="821ea-107">傳送[雲端到裝置][ lnk-c2d]回 hello 解決方案的訊息結尾 tooyour 裝置。</span><span class="sxs-lookup"><span data-stu-id="821ea-107">Sending [cloud-to-device][lnk-c2d] messages from hello solution back end tooyour devices.</span></span>

<span data-ttu-id="821ea-108">IoT 中樞傳訊功能的核心屬性是 hello 穩定性及訊息的持續性。</span><span class="sxs-lookup"><span data-stu-id="821ea-108">Core properties of IoT Hub messaging functionality are hello reliability and durability of messages.</span></span> <span data-ttu-id="821ea-109">這些屬性可讓在 hello 裝置端，彈性 toointermittent 連線和 tooload 升高 hello 雲端端處理的事件中。</span><span class="sxs-lookup"><span data-stu-id="821ea-109">These properties enable resilience toointermittent connectivity on hello device side, and tooload spikes in event processing on hello cloud side.</span></span> <span data-ttu-id="821ea-110">IoT 中樞會針對裝置到雲端和雲端到裝置訊息，實作「至少一次」  傳遞保證。</span><span class="sxs-lookup"><span data-stu-id="821ea-110">IoT Hub implements *at least once* delivery guarantees for both device-to-cloud and cloud-to-device messaging.</span></span>

<span data-ttu-id="821ea-111">IoT 中樞簡介 toohello 功能，請參閱 hello 文件[Azure 和物聯網][ lnk-azure-iot]和[hello Azure IoT 中樞服務概觀][lnk-iot-hub-overview].</span><span class="sxs-lookup"><span data-stu-id="821ea-111">For an introduction toohello capabilities of IoT Hub, see hello articles [Azure and Internet of Things][lnk-azure-iot] and [Overview of hello Azure IoT Hub service][lnk-iot-hub-overview].</span></span>

## <a name="when-toouse-iot-hub-messaging"></a><span data-ttu-id="821ea-112">當 toouse IoT 中樞通訊</span><span class="sxs-lookup"><span data-stu-id="821ea-112">When toouse IoT Hub messaging</span></span>

<span data-ttu-id="821ea-113">使用單向通知 tooyour 裝置應用程式的傳送時間數列遙測和警示您裝置的應用程式，從裝置到雲端訊息和雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="821ea-113">Use device-to-cloud messages for sending time series telemetry and alerts from your device app, and cloud-to-device messages for one-way notifications tooyour device app.</span></span>

* <span data-ttu-id="821ea-114">參照太[裝置到雲端通訊指引][ lnk-d2c-guidance]如果不確定之間使用裝置到雲端訊息、 報告的屬性或檔案上傳。</span><span class="sxs-lookup"><span data-stu-id="821ea-114">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using device-to-cloud messages, reported properties, or file upload.</span></span>
* <span data-ttu-id="821ea-115">參照太[雲端到裝置通訊指引][ lnk-c2d-guidance]如果不確定之間使用雲端到裝置訊息、 所需的屬性或直接的方法。</span><span class="sxs-lookup"><span data-stu-id="821ea-115">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using cloud-to-device messages, desired properties, or direct methods.</span></span>

## <a name="next-steps"></a><span data-ttu-id="821ea-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="821ea-116">Next steps</span></span>

* <span data-ttu-id="821ea-117">了解 IoT 中樞[裝置對雲端傳訊][lnk-d2c]。</span><span class="sxs-lookup"><span data-stu-id="821ea-117">Learn about IoT Hub [device-to-cloud messaging][lnk-d2c].</span></span>
* <span data-ttu-id="821ea-118">了解 IoT 中樞[雲端對裝置傳訊][lnk-c2d]。</span><span class="sxs-lookup"><span data-stu-id="821ea-118">Learn about IoT Hub [cloud-to-device messaging][lnk-c2d].</span></span>

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md