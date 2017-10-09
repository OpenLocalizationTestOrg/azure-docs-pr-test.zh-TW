---
title: "Azure IoT 中樞-開始連接 IoT 裝置 toohello 雲端 |Microsoft 文件"
description: "深入了解如何 tooconnect 您的 IoT 面板和入門套件 tooAzure IoT 中樞。 您的裝置可以傳送遙測 tooIoT 中樞和 IoT 中心可以監視和管理您的裝置。"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: "Azure IoT 中樞教學課程"
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: 6dc956308009091532019ff84aec881f042f0104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-tutorials"></a><span data-ttu-id="8001f-105">Azure IoT 中樞快速入門教學課程</span><span class="sxs-lookup"><span data-stu-id="8001f-105">Azure IoT Hub get started tutorials</span></span>

<span data-ttu-id="8001f-106">您可以使用 Azure IoT 中樞與 hello Azure IoT 裝置 Sdk toobuild 物聯網 (IoT) 解決方案：</span><span class="sxs-lookup"><span data-stu-id="8001f-106">You can use Azure IoT Hub and hello Azure IoT device SDKs toobuild Internet of Things (IoT) solutions:</span></span>

* <span data-ttu-id="8001f-107">Azure IoT 中樞是完全受管理的服務，可安全地連接、 監控，以及管理您的 IoT 裝置 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="8001f-107">Azure IoT Hub is a fully managed service in hello cloud that securely connects, monitors, and manages your IoT devices.</span></span> <span data-ttu-id="8001f-108">使用 hello Azure IoT 裝置 Sdk tooimplement IoT 裝置。</span><span class="sxs-lookup"><span data-stu-id="8001f-108">Use hello Azure IoT Device SDKs tooimplement your IoT devices.</span></span>
* <span data-ttu-id="8001f-109">在更複雜的 IoT 案例中使用 IoT 閘道。</span><span class="sxs-lookup"><span data-stu-id="8001f-109">Use an IoT gateway in more complex IoT scenarios.</span></span> <span data-ttu-id="8001f-110">例如，您需要 tooconsider 因素，例如 傳統裝置、 頻寬成本、 安全性和隱私權原則或邊緣資料處理。</span><span class="sxs-lookup"><span data-stu-id="8001f-110">For example, where you need tooconsider factors such as legacy devices, bandwidth costs, security and privacy policies, or edge data processing.</span></span> <span data-ttu-id="8001f-111">在這些情況下，您可以使用 Azure IoT 邊緣 tooimplement 連接裝置 tooyour IoT 中樞的閘道。</span><span class="sxs-lookup"><span data-stu-id="8001f-111">In these scenarios, you use Azure IoT Edge tooimplement a gateway that connects devices tooyour IoT hub.</span></span>

## <a name="what-hello-tutorials-cover"></a><span data-ttu-id="8001f-112">Hello 教學課程所涵蓋的功能</span><span class="sxs-lookup"><span data-stu-id="8001f-112">What hello tutorials cover</span></span>

<span data-ttu-id="8001f-113">這些教學課程介紹 tooAzure IoT 中樞和 hello 裝置 Sdk。</span><span class="sxs-lookup"><span data-stu-id="8001f-113">These tutorials introduce you tooAzure IoT Hub and hello device SDKs.</span></span> <span data-ttu-id="8001f-114">hello 教學課程涵蓋常見 IoT 案例 toodemonstrate hello 功能的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8001f-114">hello tutorials cover common IoT scenarios toodemonstrate hello capabilities of IoT Hub.</span></span> <span data-ttu-id="8001f-115">hello 教學課程也說明如何 toocombine IoT 中樞與其他 Azure 服務和工具 toobuild 更強大的 IoT 解決方案。</span><span class="sxs-lookup"><span data-stu-id="8001f-115">hello tutorials also illustrate how toocombine IoT Hub with other Azure services and tools toobuild more powerful IoT solutions.</span></span> <span data-ttu-id="8001f-116">在 hello 教學課程中，您可以選擇 toouse 模擬或實際 IoT 裝置。</span><span class="sxs-lookup"><span data-stu-id="8001f-116">In hello tutorials, you can choose toouse either simulated or real IoT devices.</span></span> <span data-ttu-id="8001f-117">此外，您可以了解如何 toouse 閘道 tooenable 裝置 tooconnect tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8001f-117">In addition, you can learn how toouse a gateway tooenable devices tooconnect tooyour IoT hub.</span></span>

## <a name="set-up-your-device"></a><span data-ttu-id="8001f-118">設定您的裝置</span><span class="sxs-lookup"><span data-stu-id="8001f-118">Set up your device</span></span>

<span data-ttu-id="8001f-119">連接 IoT 裝置或閘道 tooAzure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8001f-119">Connect an IoT device or gateway tooAzure IoT Hub.</span></span> <span data-ttu-id="8001f-120">您可以選擇啟動實體或模擬裝置 tooget:</span><span class="sxs-lookup"><span data-stu-id="8001f-120">You can choose a physical or simulated device tooget started:</span></span>

| <span data-ttu-id="8001f-121">IoT 裝置</span><span class="sxs-lookup"><span data-stu-id="8001f-121">IoT device</span></span>                       | <span data-ttu-id="8001f-122">程式設計語言</span><span class="sxs-lookup"><span data-stu-id="8001f-122">Programming language</span></span> |
|----------------------------------|----------------------|
| <span data-ttu-id="8001f-123">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="8001f-123">Raspberry Pi</span></span>                     | <span data-ttu-id="8001f-124">[Python][Pi_Py]、[Node.js][Pi_Nd]、[C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="8001f-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="8001f-125">IoT DevKit</span><span class="sxs-lookup"><span data-stu-id="8001f-125">IoT DevKit</span></span>                       | <span data-ttu-id="8001f-126">[VSCode 中的 Arduino][DevKit]</span><span class="sxs-lookup"><span data-stu-id="8001f-126">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="8001f-127">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="8001f-127">Intel Edison</span></span>                     | <span data-ttu-id="8001f-128">[Node.js][Ed_Nd]、[C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="8001f-128">[Node.js][Ed_Nd], [C][Ed_C]</span></span>    |
| <span data-ttu-id="8001f-129">Adafruit Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="8001f-129">Adafruit Feather HUZZAH ESP8266</span></span>  | <span data-ttu-id="8001f-130">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="8001f-130">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="8001f-131">Sparkfun ESP8266 Thing 開發人員</span><span class="sxs-lookup"><span data-stu-id="8001f-131">Sparkfun ESP8266 Thing Dev</span></span>       | <span data-ttu-id="8001f-132">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="8001f-132">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="8001f-133">Adafruit Feather M0</span><span class="sxs-lookup"><span data-stu-id="8001f-133">Adafruit Feather M0</span></span>              | <span data-ttu-id="8001f-134">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="8001f-134">[Arduino][M0_Ard]</span></span>              |
| <span data-ttu-id="8001f-135">電腦上的模擬的裝置</span><span class="sxs-lookup"><span data-stu-id="8001f-135">Simulated device on PC</span></span>           | <span data-ttu-id="8001f-136">[.NET][Sim_NET]、[Java][Sim_Jav]、[Node.js][Sim_Nd]、[Python][Sim_Pyth]</span><span class="sxs-lookup"><span data-stu-id="8001f-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span></span> |
| <span data-ttu-id="8001f-137">線上裝置模擬器</span><span class="sxs-lookup"><span data-stu-id="8001f-137">Online device simulator</span></span>         | <span data-ttu-id="8001f-138">[Raspberry Pi (Node.js)][Ol_Sim]</span><span class="sxs-lookup"><span data-stu-id="8001f-138">[Raspberry Pi (Node.js)][Ol_Sim]</span></span> |

<span data-ttu-id="8001f-139">此外，您可以使用 IoT 邊緣閘道 tooenable 裝置 tooconnect tooyour IoT 中心：</span><span class="sxs-lookup"><span data-stu-id="8001f-139">In addition, you can use an IoT Edge gateway tooenable devices tooconnect tooyour IoT hub:</span></span>

| <span data-ttu-id="8001f-140">閘道裝置</span><span class="sxs-lookup"><span data-stu-id="8001f-140">Gateway device</span></span>               | <span data-ttu-id="8001f-141">程式設計語言</span><span class="sxs-lookup"><span data-stu-id="8001f-141">Programming language</span></span> | <span data-ttu-id="8001f-142">平台</span><span class="sxs-lookup"><span data-stu-id="8001f-142">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="8001f-143">Intel NUC (模型 DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="8001f-143">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="8001f-144">C</span><span class="sxs-lookup"><span data-stu-id="8001f-144">C</span></span>                    | <span data-ttu-id="8001f-145">[Wind River Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="8001f-145">[Wind River Linux][NUC_Lnx]</span></span> |
| <span data-ttu-id="8001f-146">模擬閘道</span><span class="sxs-lookup"><span data-stu-id="8001f-146">Simulated gateway</span></span>            | <span data-ttu-id="8001f-147">C</span><span class="sxs-lookup"><span data-stu-id="8001f-147">C</span></span>                    | <span data-ttu-id="8001f-148">[Linux][Sim_Lnx]、[Windows][Sim_Win]</span><span class="sxs-lookup"><span data-stu-id="8001f-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span></span> |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]

[Pi_Nd]: iot-hub-raspberry-pi-kit-node-get-started.md
[Pi_C]: iot-hub-raspberry-pi-kit-c-get-started.md
[Pi_Py]: iot-hub-raspberry-pi-kit-python-get-started.md
[DevKit]: iot-hub-arduino-iot-devkit-az3166-get-started.md
[Ed_Nd]: iot-hub-intel-edison-kit-node-get-started.md
[Ed_C]: iot-hub-intel-edison-kit-c-get-started.md
[Hu_Ard]: iot-hub-arduino-huzzah-esp8266-get-started.md
[Th_Ard]: iot-hub-sparkfun-esp8266-thing-dev-get-started.md
[M0_Ard]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
[Ol_Sim]: iot-hub-raspberry-pi-web-simulator-get-started.md
