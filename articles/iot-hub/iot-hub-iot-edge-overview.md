---
title: "Azure IoT 邊緣的 aaaOverview |Microsoft 文件"
description: "描述 hello 架構的關鍵概念 Azure IoT 邊緣閘道、 模組和代理程式等。"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: 32debc0d4f40cfd7f2cce7cf8c76b12ec18ee2dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a><span data-ttu-id="d1d0a-103">Azure IoT Edge 架構概念</span><span class="sxs-lookup"><span data-stu-id="d1d0a-103">Azure IoT Edge architectural concepts</span></span>

<span data-ttu-id="d1d0a-104">您檢查任何範例程式碼，或建立您自己使用 IoT 邊緣的欄位閘道之前，您應該了解 hello underpin IoT 邊緣 hello 架構的重要概念。</span><span class="sxs-lookup"><span data-stu-id="d1d0a-104">Before you examine any sample code or create your own field gateway using IoT Edge, you should understand hello key concepts that underpin hello architecture of IoT Edge.</span></span>

## <a name="iot-edge-modules"></a><span data-ttu-id="d1d0a-105">IoT Edge 模組</span><span class="sxs-lookup"><span data-stu-id="d1d0a-105">IoT Edge modules</span></span>

<span data-ttu-id="d1d0a-106">建立和組合「IoT Edge 模組」，即可使用 Azure IoT Edge 來建置閘道。</span><span class="sxs-lookup"><span data-stu-id="d1d0a-106">You build a gateway with Azure IoT Edge by creating and assembling *IoT Edge modules*.</span></span> <span data-ttu-id="d1d0a-107">模組使用*訊息*tooexchange 彼此的資料。</span><span class="sxs-lookup"><span data-stu-id="d1d0a-107">Modules use *messages* tooexchange data with each other.</span></span> <span data-ttu-id="d1d0a-108">模組接收訊息、 執行一些動作，選擇性地將它轉換成新的訊息，且然後發行它的其他模組 tooprocess。</span><span class="sxs-lookup"><span data-stu-id="d1d0a-108">A module receives a message, performs some action on it, optionally transforms it into a new message, and then publishes it for other modules tooprocess.</span></span> <span data-ttu-id="d1d0a-109">某些模組可能只會產生新的訊息，且永遠不會處理內送訊息。</span><span class="sxs-lookup"><span data-stu-id="d1d0a-109">Some modules might only produce new messages and never process incoming messages.</span></span> <span data-ttu-id="d1d0a-110">模組的鏈結會在一處，該管線中的 hello 資料上執行轉換每個模組建立資料處理管線。</span><span class="sxs-lookup"><span data-stu-id="d1d0a-110">A chain of modules creates a data processing pipeline with each module performing a transformation on hello data at one point in that pipeline.</span></span>

![使用 Azure IoT Edge 所建置之閘道中的模組鏈結][1]

<span data-ttu-id="d1d0a-112">IoT 邊緣包含下列元件的 hello:</span><span class="sxs-lookup"><span data-stu-id="d1d0a-112">IoT Edge contains hello following components:</span></span>

* <span data-ttu-id="d1d0a-113">可執行常見閘道函式的預先撰寫模組。</span><span class="sxs-lookup"><span data-stu-id="d1d0a-113">Pre-written modules that perform common gateway functions.</span></span>
* <span data-ttu-id="d1d0a-114">hello 介面的開發人員可以使用 toowrite 自訂模組。</span><span class="sxs-lookup"><span data-stu-id="d1d0a-114">hello interfaces a developer can use toowrite custom modules.</span></span>
* <span data-ttu-id="d1d0a-115">hello 基礎結構需要 toodeploy 和執行模組的設定。</span><span class="sxs-lookup"><span data-stu-id="d1d0a-115">hello infrastructure necessary toodeploy and run a set of modules.</span></span>

<span data-ttu-id="d1d0a-116">hello SDK 提供一個抽象層，可讓您 toobuild 閘道 toorun 各種作業系統與平台上。</span><span class="sxs-lookup"><span data-stu-id="d1d0a-116">hello SDK provides an abstraction layer that enables you toobuild gateways toorun on various operating systems and platforms.</span></span>

![Azure IoT Edge 抽象層][2]

## <a name="messages"></a><span data-ttu-id="d1d0a-118">訊息</span><span class="sxs-lookup"><span data-stu-id="d1d0a-118">Messages</span></span>

<span data-ttu-id="d1d0a-119">雖然改善模組傳遞的郵件 tooeach 其他很方便的方式 tooconceptualize 閘道函式，它不會精確地反映會發生什麼事。</span><span class="sxs-lookup"><span data-stu-id="d1d0a-119">Although thinking about modules passing messages tooeach other is a convenient way tooconceptualize how a gateway functions, it does not accurately reflect what happens.</span></span> <span data-ttu-id="d1d0a-120">IoT 邊緣模組使用 broker toocommunicate 彼此。</span><span class="sxs-lookup"><span data-stu-id="d1d0a-120">IoT Edge modules use a broker toocommunicate with each other.</span></span> <span data-ttu-id="d1d0a-121">模組發佈訊息 toohello broker （使用例如匯流排上，或發行/訂閱傳訊模式），然後讓 hello broker 路由 hello 訊息 toohello 模組連接的 tooit。</span><span class="sxs-lookup"><span data-stu-id="d1d0a-121">Modules publish messages toohello broker (using messaging patterns such as bus, or publish/subscribe) and then let hello broker route hello message toohello modules connected tooit.</span></span>

<span data-ttu-id="d1d0a-122">模組會使用 hello **Broker_Publish**函式 toopublish 訊息 toohello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="d1d0a-122">A module uses hello **Broker_Publish** function toopublish a message toohello broker.</span></span> <span data-ttu-id="d1d0a-123">hello broker 也會藉由叫用的回呼函式傳遞訊息 tooa 模組。</span><span class="sxs-lookup"><span data-stu-id="d1d0a-123">hello broker delivers messages tooa module by invoking a callback function.</span></span> <span data-ttu-id="d1d0a-124">訊息包含一組索引鍵/值屬性以及傳遞為記憶體區塊的內容。</span><span class="sxs-lookup"><span data-stu-id="d1d0a-124">A message consists of a set of key/value properties and content passed as a block of memory.</span></span>

![hello Broker Azure IoT Edge 中的 hello 角色][3]

## <a name="message-routing-and-filtering"></a><span data-ttu-id="d1d0a-126">訊息路由和篩選</span><span class="sxs-lookup"><span data-stu-id="d1d0a-126">Message routing and filtering</span></span>

<span data-ttu-id="d1d0a-127">有兩種方式 toodirect 訊息 toohello 正確 IoT 邊緣模組：</span><span class="sxs-lookup"><span data-stu-id="d1d0a-127">There are two ways toodirect messages toohello correct IoT Edge modules:</span></span>

* <span data-ttu-id="d1d0a-128">您可以將傳遞的一組連結可以傳遞 toohello broker 讓 hello broker 知道 hello 來源和接收的每個模組。</span><span class="sxs-lookup"><span data-stu-id="d1d0a-128">You can pass a set of links can be passed toohello broker so hello broker knows hello source and sink for each module.</span></span>
* <span data-ttu-id="d1d0a-129">模組可以篩選 hello hello 訊息屬性。</span><span class="sxs-lookup"><span data-stu-id="d1d0a-129">A module can filter on hello properties of hello message.</span></span>

<span data-ttu-id="d1d0a-130">如果 hello 訊息用於訊息只應處理模組。</span><span class="sxs-lookup"><span data-stu-id="d1d0a-130">A module should only act upon a message if hello message is intended for it.</span></span> <span data-ttu-id="d1d0a-131">連結和訊息篩選可有效地建立訊息管線。</span><span class="sxs-lookup"><span data-stu-id="d1d0a-131">Links and message filtering effectively create a message pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1d0a-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d1d0a-132">Next steps</span></span>

<span data-ttu-id="d1d0a-133">請參閱 toosee 套用在範例中，您可以執行這些概念[瀏覽 Azure IoT 邊緣架構][lnk-hello-world]。</span><span class="sxs-lookup"><span data-stu-id="d1d0a-133">toosee these concepts applied in a sample you can run, see [Explore Azure IoT Edge architecture][lnk-hello-world].</span></span>

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md