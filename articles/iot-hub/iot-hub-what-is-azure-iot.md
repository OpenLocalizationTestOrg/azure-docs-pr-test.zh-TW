---
title: "物聯網 （IoT 套件） 的 aaaAzure 解決方案 |Microsoft 文件"
description: "概觀範例 IoT 解決方案架構，以及它與 toodevices，hello Azure IoT 中樞服務、 Azure IoT 裝置 Sdk、 Azure IoT 服務 Sdk 和其他 Azure 服務。"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a859e379-dca7-42fa-bdf6-1125c86ad140
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 2d934e3f988c530de6a242869c021712d2aa1576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="next-steps"></a><span data-ttu-id="3e742-103">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3e742-103">Next steps</span></span>

<span data-ttu-id="3e742-104">Azure IoT 中樞是一項 Azure 服務，可讓解決方案後端與數百萬個裝置進行安全可靠的雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="3e742-104">Azure IoT Hub is an Azure service that enables secure and reliable bi-directional communications between your solution back end and millions of devices.</span></span> <span data-ttu-id="3e742-105">它可讓 hello 方案後的端：</span><span class="sxs-lookup"><span data-stu-id="3e742-105">It enables hello solution back end to:</span></span>

* <span data-ttu-id="3e742-106">從您的裝置接收大規模遙測。</span><span class="sxs-lookup"><span data-stu-id="3e742-106">Receive telemetry at scale from your devices.</span></span>
* <span data-ttu-id="3e742-107">從您的裝置 tooa 資料流的事件處理器的路由資料。</span><span class="sxs-lookup"><span data-stu-id="3e742-107">Route data from your devices tooa stream event processor.</span></span>
* <span data-ttu-id="3e742-108">從裝置接收檔案上傳。</span><span class="sxs-lookup"><span data-stu-id="3e742-108">Receive file uploads from devices.</span></span>
* <span data-ttu-id="3e742-109">將雲端到裝置訊息傳送 toospecific 裝置。</span><span class="sxs-lookup"><span data-stu-id="3e742-109">Send cloud-to-device messages toospecific devices.</span></span>

<span data-ttu-id="3e742-110">您可以使用 IoT 中樞 tooimplement 結束回到您自己的解決方案。</span><span class="sxs-lookup"><span data-stu-id="3e742-110">You can use IoT Hub tooimplement your own solution back end.</span></span> <span data-ttu-id="3e742-111">此外，IoT 中樞會包含身分識別登錄使用 tooprovision 裝置、 他們的安全性認證和其權限 tooconnect toohello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3e742-111">In addition, IoT Hub includes an identity registry used tooprovision devices, their security credentials, and their rights tooconnect toohello IoT hub.</span></span> <span data-ttu-id="3e742-112">toolearn 深入了解 IoT 中樞，請參閱[IoT 中樞是什麼？][lnk-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="3e742-112">toolearn more about IoT Hub, see [What is IoT Hub?][lnk-iot-hub].</span></span>

<span data-ttu-id="3e742-113">toolearn 如何 Azure IoT 中樞可讓標準為基礎的裝置管理，針對您 tooremotely 管理、 設定及更新您的裝置，請參閱[裝置管理概觀與 IoT 中樞][lnk-device-management]。</span><span class="sxs-lookup"><span data-stu-id="3e742-113">toolearn how Azure IoT Hub enables standards-based device management for you tooremotely manage, configure, and update your devices, see [Overview of device management with IoT Hub][lnk-device-management].</span></span>

<span data-ttu-id="3e742-114">tooimplement 各種裝置的硬體平台和作業系統上的用戶端應用程式，您可以使用 hello Azure IoT 裝置 Sdk。</span><span class="sxs-lookup"><span data-stu-id="3e742-114">tooimplement client applications on a wide variety of device hardware platforms and operating systems, you can use hello Azure IoT device SDKs.</span></span> <span data-ttu-id="3e742-115">hello 裝置 Sdk 包含程式庫，以便傳送遙測 tooan IoT 中樞與接收雲端到裝置的訊息。</span><span class="sxs-lookup"><span data-stu-id="3e742-115">hello device SDKs include libraries that facilitate sending telemetry tooan IoT hub and receiving cloud-to-device messages.</span></span> <span data-ttu-id="3e742-116">當您使用 hello 裝置 Sdk 時，您可以選擇從數個網路通訊協定 toocommunicate 與 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3e742-116">When you use hello device SDKs, you can choose from several network protocols toocommunicate with IoT Hub.</span></span> <span data-ttu-id="3e742-117">toolearn 詳細資訊，請參閱 hello[裝置 Sdk 的相關資訊][lnk-device-sdks]。</span><span class="sxs-lookup"><span data-stu-id="3e742-117">toolearn more, see hello [information about device SDKs][lnk-device-sdks].</span></span>

<span data-ttu-id="3e742-118">tooget 啟動撰寫一些程式碼，並執行一些範例，請參閱 hello[開始使用 IoT 中樞][ lnk-getstarted]教學課程。</span><span class="sxs-lookup"><span data-stu-id="3e742-118">tooget started writing some code and running some samples, see hello [Get started with IoT Hub][lnk-getstarted] tutorial.</span></span>

<span data-ttu-id="3e742-119">您也可能會對 [Azure IoT 套件][lnk-iot-suite]有興趣，這是預先設定的解決方案集合。</span><span class="sxs-lookup"><span data-stu-id="3e742-119">You may also be interested in [Azure IoT Suite][lnk-iot-suite], which is a collection of preconfigured solutions.</span></span> <span data-ttu-id="3e742-120">IoT 套件可讓您 tooget 快速地開始，並調整規模 IoT 專案 tooaddress 常見 IoT 案例-例如遠端監視、 資產管理，以及預測性維護。</span><span class="sxs-lookup"><span data-stu-id="3e742-120">IoT Suite enables you tooget started quickly and scale IoT projects tooaddress common IoT scenarios--such as remote monitoring, asset management, and predictive maintenance.</span></span>

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md
