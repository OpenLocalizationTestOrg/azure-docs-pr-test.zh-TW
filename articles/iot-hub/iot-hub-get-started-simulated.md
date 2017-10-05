---
title: "開始將模擬裝置連線到 Azure IoT 中樞 | Microsoft Docs"
description: "了解如何建立模擬 IoT 裝置，並將它們連線至 Azure IoT 中樞。 您的裝置可以將遙測資料傳送到 IoT 中樞，而 IoT 中樞會監視並管理您的裝置。"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: "Azure IoT 中樞教學課程"
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: 436b3057509a831837159e814490959a2d7455a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-hub-get-started-with-simulated-devices-tutorials"></a><span data-ttu-id="81245-105">Azure IoT 中樞開始使用模擬裝置教學課程</span><span class="sxs-lookup"><span data-stu-id="81245-105">Azure IoT Hub get started with simulated devices tutorials</span></span>

<span data-ttu-id="81245-106">這些教學課程將為您介紹 Azure IoT 中樞與裝置的 SDK。</span><span class="sxs-lookup"><span data-stu-id="81245-106">These tutorials introduce you to Azure IoT Hub and the device SDKs.</span></span> <span data-ttu-id="81245-107">這些教學課程涵蓋的常見 IoT 案例會說明 IoT 中樞的功能。</span><span class="sxs-lookup"><span data-stu-id="81245-107">The tutorials cover common IoT scenarios to demonstrate the capabilities of IoT Hub.</span></span> <span data-ttu-id="81245-108">教學課程也將說明如何將 IoT 中樞與其他 Azure 服務和工具結合，建置更強大的 IoT 解決方案。</span><span class="sxs-lookup"><span data-stu-id="81245-108">The tutorials also illustrate how to combine IoT Hub with other Azure services and tools to build more powerful IoT solutions.</span></span> <span data-ttu-id="81245-109">下表所列的教學課程會示範如何建立模擬的 IoT 裝置。</span><span class="sxs-lookup"><span data-stu-id="81245-109">The tutorials listed in the following table show you how to create simulated IoT devices.</span></span>

| <span data-ttu-id="81245-110">程式設計語言</span><span class="sxs-lookup"><span data-stu-id="81245-110">Programming language</span></span> |
|----------------------|
| <span data-ttu-id="81245-111">[.NET][Sim_NET]</span><span class="sxs-lookup"><span data-stu-id="81245-111">[.NET][Sim_NET]</span></span>      |
| <span data-ttu-id="81245-112">[Java][Sim_Jav]</span><span class="sxs-lookup"><span data-stu-id="81245-112">[Java][Sim_Jav]</span></span>      |
| <span data-ttu-id="81245-113">[Node.js][Sim_Nd]</span><span class="sxs-lookup"><span data-stu-id="81245-113">[Node.js][Sim_Nd]</span></span>    |
| <span data-ttu-id="81245-114">[Python][Sim_Pyth]</span><span class="sxs-lookup"><span data-stu-id="81245-114">[Python][Sim_Pyth]</span></span>   |

<span data-ttu-id="81245-115">此外，您可以使用 IoT Edge 閘道來讓模擬的裝置連線到您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="81245-115">In addition, you can use an IoT Edge gateway to enable simulated devices to connect to your IoT hub.</span></span>

| <span data-ttu-id="81245-116">程式設計語言</span><span class="sxs-lookup"><span data-stu-id="81245-116">Programming language</span></span> | <span data-ttu-id="81245-117">平台</span><span class="sxs-lookup"><span data-stu-id="81245-117">Platform</span></span>           |
|----------------------|------------------- |
| <span data-ttu-id="81245-118">C</span><span class="sxs-lookup"><span data-stu-id="81245-118">C</span></span>                    | <span data-ttu-id="81245-119">[Linux][Sim_Lnx]</span><span class="sxs-lookup"><span data-stu-id="81245-119">[Linux][Sim_Lnx]</span></span>   |
| <span data-ttu-id="81245-120">C</span><span class="sxs-lookup"><span data-stu-id="81245-120">C</span></span>                    | <span data-ttu-id="81245-121">[Windows][Sim_Win]</span><span class="sxs-lookup"><span data-stu-id="81245-121">[Windows][Sim_Win]</span></span> |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]

[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
