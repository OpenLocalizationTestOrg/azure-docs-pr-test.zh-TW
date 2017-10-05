---
title: "將 Raspberry Pi 連線至 Azure IoT 套件 | Microsoft Docs"
description: "教學課程使用 Node.js 或 C 來幫助您了解如何使用 Raspberry Pi 3 的 Microsoft Azure IoT 入門套件，以及遠端監視解決方案的 IoT 套件。 您可以選擇的教學課程包括模擬遙測、使用真實感應器，或更新遠端韌體。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: eaa6a21a08bd9068b5335a8167f54c2aa387e0e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-microsoft-azure-iot-raspberry-pi-3-starter-kit-to-the-remote-monitoring-solution"></a><span data-ttu-id="ad12f-104">將 Microsoft Azure IoT Raspberry Pi 3 入門套件連線到遠端監視解決方案</span><span class="sxs-lookup"><span data-stu-id="ad12f-104">Connect your Microsoft Azure IoT Raspberry Pi 3 Starter Kit to the remote monitoring solution</span></span>

<span data-ttu-id="ad12f-105">本章節的教學課程可協助您了解如何將 Raspberry Pi 3 裝置連線到遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="ad12f-105">The tutorials in this section help you learn how to connect a Raspberry Pi 3 device to the remote monitoring solution.</span></span> <span data-ttu-id="ad12f-106">選擇適合您偏好程式設計語言的教學課程，以及您是否有可搭配 Raspberry Pi 使用的感應器硬體。</span><span class="sxs-lookup"><span data-stu-id="ad12f-106">Choose the tutorial appropriate to your preferred programming language and the whether you have the sensor hardware available to use with your Raspberry Pi.</span></span>

## <a name="the-tutorials"></a><span data-ttu-id="ad12f-107">教學課程</span><span class="sxs-lookup"><span data-stu-id="ad12f-107">The tutorials</span></span>

| <span data-ttu-id="ad12f-108">教學課程</span><span class="sxs-lookup"><span data-stu-id="ad12f-108">Tutorial</span></span> | <span data-ttu-id="ad12f-109">注意事項</span><span class="sxs-lookup"><span data-stu-id="ad12f-109">Notes</span></span> | <span data-ttu-id="ad12f-110">語言</span><span class="sxs-lookup"><span data-stu-id="ad12f-110">Languages</span></span> |
| -------- | ----- | --------- |
| <span data-ttu-id="ad12f-111">模擬遙測 (基本)</span><span class="sxs-lookup"><span data-stu-id="ad12f-111">Simulated telemetry (Basic)</span></span>| <span data-ttu-id="ad12f-112">模擬感應器資料。</span><span class="sxs-lookup"><span data-stu-id="ad12f-112">Simulates sensor data.</span></span> <span data-ttu-id="ad12f-113">使用獨立 Raspberry Pi。</span><span class="sxs-lookup"><span data-stu-id="ad12f-113">Uses a standalone Raspberry Pi.</span></span> | <span data-ttu-id="ad12f-114">[C][lnk-c-simulator]、[Node.js][lnk-node-simulator]</span><span class="sxs-lookup"><span data-stu-id="ad12f-114">[C][lnk-c-simulator], [Node.js][lnk-node-simulator]</span></span> |
| <span data-ttu-id="ad12f-115">真實感應器 (中級)</span><span class="sxs-lookup"><span data-stu-id="ad12f-115">Real sensor (Intermediate)</span></span> | <span data-ttu-id="ad12f-116">使用連線到 Raspberry Pi 之 BME280 感應器的資料。</span><span class="sxs-lookup"><span data-stu-id="ad12f-116">Uses data from a BME280 sensor connected to your Raspberry Pi.</span></span> | <span data-ttu-id="ad12f-117">[C][lnk-c-basic]、[Node.js][lnk-node-basic]</span><span class="sxs-lookup"><span data-stu-id="ad12f-117">[C][lnk-c-basic], [Node.js][lnk-node-basic]</span></span> |
| <span data-ttu-id="ad12f-118">實作韌體更新 (進階)</span><span class="sxs-lookup"><span data-stu-id="ad12f-118">Implement firmware update (Advanced)</span></span>| <span data-ttu-id="ad12f-119">使用連線到 Raspberry Pi 之 BME280 感應器的資料。</span><span class="sxs-lookup"><span data-stu-id="ad12f-119">Uses data from a BME280 sensor connected to your Raspberry Pi.</span></span> <span data-ttu-id="ad12f-120">啟用 Raspberry Pi 上的遠端韌體更新。</span><span class="sxs-lookup"><span data-stu-id="ad12f-120">Enables remote firmware updates on your Raspberry Pi.</span></span> | <span data-ttu-id="ad12f-121">[C][lnk-c-advanced]、[Node.js][lnk-node-advanced]</span><span class="sxs-lookup"><span data-stu-id="ad12f-121">[C][lnk-c-advanced], [Node.js][lnk-node-advanced]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ad12f-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ad12f-122">Next steps</span></span>

<span data-ttu-id="ad12f-123">請瀏覽 [Azure IoT 開發人員中心](https://azure.microsoft.com/develop/iot/)，取得更多 Azure IoT 的相關範例和文件。</span><span class="sxs-lookup"><span data-stu-id="ad12f-123">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[lnk-node-simulator]: iot-suite-raspberry-pi-kit-node-get-started-simulator.md
[lnk-node-basic]: iot-suite-raspberry-pi-kit-node-get-started-basic.md
[lnk-node-advanced]: iot-suite-raspberry-pi-kit-node-get-started-advanced.md
[lnk-c-simulator]: iot-suite-raspberry-pi-kit-c-get-started-simulator.md
[lnk-c-basic]: iot-suite-raspberry-pi-kit-c-get-started-basic.md
[lnk-c-advanced]: iot-suite-raspberry-pi-kit-c-get-started-advanced.md