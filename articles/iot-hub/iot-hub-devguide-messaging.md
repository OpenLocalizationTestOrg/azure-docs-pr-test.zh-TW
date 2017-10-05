---
title: "了解 Azure IoT 中樞傳訊 | Microsoft Docs"
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
ms.openlocfilehash: f54398d7ac46bf178d2bb603669b399d25370736
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a><span data-ttu-id="526b3-104">IoT 中樞的裝置到雲端及雲端到裝置傳訊</span><span class="sxs-lookup"><span data-stu-id="526b3-104">Device-to-cloud and cloud-to-device messaging with IoT Hub</span></span>

<span data-ttu-id="526b3-105">使用 IoT 中樞傳訊以下列方式與您的裝置通訊：</span><span class="sxs-lookup"><span data-stu-id="526b3-105">Use IoT Hub messaging to communicate with your devices by:</span></span>

* <span data-ttu-id="526b3-106">從您的裝置傳送[裝置對雲端][lnk-d2c]訊息到您的解決方案後端。</span><span class="sxs-lookup"><span data-stu-id="526b3-106">Sending [device-to-cloud][lnk-d2c] messages from your devices to your solution back end.</span></span>
* <span data-ttu-id="526b3-107">從解決方案後端傳送[雲端對裝置][lnk-c2d]訊息到您的裝置。</span><span class="sxs-lookup"><span data-stu-id="526b3-107">Sending [cloud-to-device][lnk-c2d] messages from the solution back end to your devices.</span></span>

<span data-ttu-id="526b3-108">IoT 中樞傳訊功能的核心屬性是訊息的可靠性和持久性。</span><span class="sxs-lookup"><span data-stu-id="526b3-108">Core properties of IoT Hub messaging functionality are the reliability and durability of messages.</span></span> <span data-ttu-id="526b3-109">這些屬性可在裝置端上恢復間歇性連線，以及在雲端恢復事件處理的負載尖峰。</span><span class="sxs-lookup"><span data-stu-id="526b3-109">These properties enable resilience to intermittent connectivity on the device side, and to load spikes in event processing on the cloud side.</span></span> <span data-ttu-id="526b3-110">IoT 中樞會針對裝置到雲端和雲端到裝置訊息，實作「至少一次」  傳遞保證。</span><span class="sxs-lookup"><span data-stu-id="526b3-110">IoT Hub implements *at least once* delivery guarantees for both device-to-cloud and cloud-to-device messaging.</span></span>

<span data-ttu-id="526b3-111">如需 IoT 中樞功能的簡介，請參閱 [Azure 和物聯網][lnk-azure-iot]及 [Azure IoT 中樞服務的概觀][lnk-iot-hub-overview]等文章。</span><span class="sxs-lookup"><span data-stu-id="526b3-111">For an introduction to the capabilities of IoT Hub, see the articles [Azure and Internet of Things][lnk-azure-iot] and [Overview of the Azure IoT Hub service][lnk-iot-hub-overview].</span></span>

## <a name="when-to-use-iot-hub-messaging"></a><span data-ttu-id="526b3-112">使用 IoT 中樞傳訊時</span><span class="sxs-lookup"><span data-stu-id="526b3-112">When to use IoT Hub messaging</span></span>

<span data-ttu-id="526b3-113">使用裝置到雲端訊息可傳送裝置應用程式所傳來的時間序列遙測和警示，使用雲端到裝置訊息則可用來傳送單向通知給您的裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="526b3-113">Use device-to-cloud messages for sending time series telemetry and alerts from your device app, and cloud-to-device messages for one-way notifications to your device app.</span></span>

* <span data-ttu-id="526b3-114">如果不確定要使用裝置對雲端訊息、回報屬性或檔案上傳，請參閱[裝置到雲端通訊指引][lnk-d2c-guidance]。</span><span class="sxs-lookup"><span data-stu-id="526b3-114">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using device-to-cloud messages, reported properties, or file upload.</span></span>
* <span data-ttu-id="526b3-115">如果不確定要使用雲端對裝置訊息、預期屬性或直接方法，請參閱[雲端到裝置通訊指引][lnk-c2d-guidance]。</span><span class="sxs-lookup"><span data-stu-id="526b3-115">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using cloud-to-device messages, desired properties, or direct methods.</span></span>

## <a name="next-steps"></a><span data-ttu-id="526b3-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="526b3-116">Next steps</span></span>

* <span data-ttu-id="526b3-117">了解 IoT 中樞[裝置對雲端傳訊][lnk-d2c]。</span><span class="sxs-lookup"><span data-stu-id="526b3-117">Learn about IoT Hub [device-to-cloud messaging][lnk-d2c].</span></span>
* <span data-ttu-id="526b3-118">了解 IoT 中樞[雲端對裝置傳訊][lnk-c2d]。</span><span class="sxs-lookup"><span data-stu-id="526b3-118">Learn about IoT Hub [cloud-to-device messaging][lnk-c2d].</span></span>

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md