---
title: "Azure IoT 中樞 - 開始將 IoT 裝置連線到雲端 | Microsoft Docs"
description: "了解如何將 IoT 面板和入門套件連線到 Azure IoT 中樞。 您的裝置可以將遙測資料傳送到 IoT 中樞，而 IoT 中樞會監視並管理您的裝置。"
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
ms.openlocfilehash: 45016e6383761ffe78f13ccef1112ab3d9753498
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-iot-hub-get-started-tutorials"></a><span data-ttu-id="f4226-105">Azure IoT 中樞快速入門教學課程</span><span class="sxs-lookup"><span data-stu-id="f4226-105">Azure IoT Hub get started tutorials</span></span>

<span data-ttu-id="f4226-106">您可以使用 Azure IoT 中樞和 Azure IoT 裝置 SDK 來建置物聯網 (IoT) 解決方案：</span><span class="sxs-lookup"><span data-stu-id="f4226-106">You can use Azure IoT Hub and the Azure IoT device SDKs to build Internet of Things (IoT) solutions:</span></span>

* <span data-ttu-id="f4226-107">Azure IoT 中樞是雲端中完全受管理的服務，可安全地連線、監視及管理您的 IoT 裝置。</span><span class="sxs-lookup"><span data-stu-id="f4226-107">Azure IoT Hub is a fully managed service in the cloud that securely connects, monitors, and manages your IoT devices.</span></span> <span data-ttu-id="f4226-108">您可以使用 Azure IoT 裝置 SDK 來實作您的 IoT 裝置。</span><span class="sxs-lookup"><span data-stu-id="f4226-108">Use the Azure IoT Device SDKs to implement your IoT devices.</span></span>
* <span data-ttu-id="f4226-109">在更複雜的 IoT 案例中使用 IoT 閘道。</span><span class="sxs-lookup"><span data-stu-id="f4226-109">Use an IoT gateway in more complex IoT scenarios.</span></span> <span data-ttu-id="f4226-110">例如，您在此案例中必須考慮諸如傳統裝置、頻寬成本、安全性和隱私權原則或邊緣資料處理等因素。</span><span class="sxs-lookup"><span data-stu-id="f4226-110">For example, where you need to consider factors such as legacy devices, bandwidth costs, security and privacy policies, or edge data processing.</span></span> <span data-ttu-id="f4226-111">在這些情況下，您可以使用 Azure IoT Edge 來實作閘道以將裝置連線到 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f4226-111">In these scenarios, you use Azure IoT Edge to implement a gateway that connects devices to your IoT hub.</span></span>

## <a name="what-the-tutorials-cover"></a><span data-ttu-id="f4226-112">這些教學課程的涵蓋範圍</span><span class="sxs-lookup"><span data-stu-id="f4226-112">What the tutorials cover</span></span>

<span data-ttu-id="f4226-113">這些教學課程將為您介紹 Azure IoT 中樞與裝置的 SDK。</span><span class="sxs-lookup"><span data-stu-id="f4226-113">These tutorials introduce you to Azure IoT Hub and the device SDKs.</span></span> <span data-ttu-id="f4226-114">這些教學課程涵蓋的常見 IoT 案例會說明 IoT 中樞的功能。</span><span class="sxs-lookup"><span data-stu-id="f4226-114">The tutorials cover common IoT scenarios to demonstrate the capabilities of IoT Hub.</span></span> <span data-ttu-id="f4226-115">教學課程也將說明如何將 IoT 中樞與其他 Azure 服務和工具結合，建置更強大的 IoT 解決方案。</span><span class="sxs-lookup"><span data-stu-id="f4226-115">The tutorials also illustrate how to combine IoT Hub with other Azure services and tools to build more powerful IoT solutions.</span></span> <span data-ttu-id="f4226-116">在教學課程中，您可以選擇使用模擬或實際的 IoT 裝置。</span><span class="sxs-lookup"><span data-stu-id="f4226-116">In the tutorials, you can choose to use either simulated or real IoT devices.</span></span> <span data-ttu-id="f4226-117">此外，您可以了解如何使用閘道來將裝置連線到您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f4226-117">In addition, you can learn how to use a gateway to enable devices to connect to your IoT hub.</span></span>

## <a name="set-up-your-device"></a><span data-ttu-id="f4226-118">設定您的裝置</span><span class="sxs-lookup"><span data-stu-id="f4226-118">Set up your device</span></span>

<span data-ttu-id="f4226-119">將 IoT 裝置或閘道連線至 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f4226-119">Connect an IoT device or gateway to Azure IoT Hub.</span></span> <span data-ttu-id="f4226-120">您可以選擇要開始使用的實體或模擬裝置：</span><span class="sxs-lookup"><span data-stu-id="f4226-120">You can choose a physical or simulated device to get started:</span></span>

| <span data-ttu-id="f4226-121">IoT 裝置</span><span class="sxs-lookup"><span data-stu-id="f4226-121">IoT device</span></span>                       | <span data-ttu-id="f4226-122">程式設計語言</span><span class="sxs-lookup"><span data-stu-id="f4226-122">Programming language</span></span> |
|----------------------------------|----------------------|
| <span data-ttu-id="f4226-123">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="f4226-123">Raspberry Pi</span></span>                     | <span data-ttu-id="f4226-124">[Python][Pi_Py]、[Node.js][Pi_Nd]、[C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="f4226-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="f4226-125">IoT DevKit</span><span class="sxs-lookup"><span data-stu-id="f4226-125">IoT DevKit</span></span>                       | <span data-ttu-id="f4226-126">[VSCode 中的 Arduino][DevKit]</span><span class="sxs-lookup"><span data-stu-id="f4226-126">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="f4226-127">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="f4226-127">Intel Edison</span></span>                     | <span data-ttu-id="f4226-128">[Node.js][Ed_Nd]、[C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="f4226-128">[Node.js][Ed_Nd], [C][Ed_C]</span></span>    |
| <span data-ttu-id="f4226-129">Adafruit Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="f4226-129">Adafruit Feather HUZZAH ESP8266</span></span>  | <span data-ttu-id="f4226-130">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="f4226-130">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="f4226-131">Sparkfun ESP8266 Thing 開發人員</span><span class="sxs-lookup"><span data-stu-id="f4226-131">Sparkfun ESP8266 Thing Dev</span></span>       | <span data-ttu-id="f4226-132">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="f4226-132">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="f4226-133">Adafruit Feather M0</span><span class="sxs-lookup"><span data-stu-id="f4226-133">Adafruit Feather M0</span></span>              | <span data-ttu-id="f4226-134">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="f4226-134">[Arduino][M0_Ard]</span></span>              |
| <span data-ttu-id="f4226-135">電腦上的模擬的裝置</span><span class="sxs-lookup"><span data-stu-id="f4226-135">Simulated device on PC</span></span>           | <span data-ttu-id="f4226-136">[.NET][Sim_NET]、[Java][Sim_Jav]、[Node.js][Sim_Nd]、[Python][Sim_Pyth]</span><span class="sxs-lookup"><span data-stu-id="f4226-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span></span> |
| <span data-ttu-id="f4226-137">線上裝置模擬器</span><span class="sxs-lookup"><span data-stu-id="f4226-137">Online device simulator</span></span>         | <span data-ttu-id="f4226-138">[Raspberry Pi (Node.js)][Ol_Sim]</span><span class="sxs-lookup"><span data-stu-id="f4226-138">[Raspberry Pi (Node.js)][Ol_Sim]</span></span> |

<span data-ttu-id="f4226-139">此外，您可以使用 IoT Edge 閘道來將裝置連線到您的 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="f4226-139">In addition, you can use an IoT Edge gateway to enable devices to connect to your IoT hub:</span></span>

| <span data-ttu-id="f4226-140">閘道裝置</span><span class="sxs-lookup"><span data-stu-id="f4226-140">Gateway device</span></span>               | <span data-ttu-id="f4226-141">程式設計語言</span><span class="sxs-lookup"><span data-stu-id="f4226-141">Programming language</span></span> | <span data-ttu-id="f4226-142">平台</span><span class="sxs-lookup"><span data-stu-id="f4226-142">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="f4226-143">Intel NUC (模型 DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="f4226-143">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="f4226-144">C</span><span class="sxs-lookup"><span data-stu-id="f4226-144">C</span></span>                    | <span data-ttu-id="f4226-145">[Wind River Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="f4226-145">[Wind River Linux][NUC_Lnx]</span></span> |
| <span data-ttu-id="f4226-146">模擬閘道</span><span class="sxs-lookup"><span data-stu-id="f4226-146">Simulated gateway</span></span>            | <span data-ttu-id="f4226-147">C</span><span class="sxs-lookup"><span data-stu-id="f4226-147">C</span></span>                    | <span data-ttu-id="f4226-148">[Linux][Sim_Lnx]、[Windows][Sim_Win]</span><span class="sxs-lookup"><span data-stu-id="f4226-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span></span> |

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
