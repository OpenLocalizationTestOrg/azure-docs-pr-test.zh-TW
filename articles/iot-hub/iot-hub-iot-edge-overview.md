---
title: "Azure IoT Edge 概觀 | Microsoft Docs"
description: "說明諸如閘道、模組和代理程式等 Azure IoT Edge 中的重要架構概念。"
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
ms.openlocfilehash: ecdd56c91a8fc2011b3d7abe93b9d27c1e1e0bef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a><span data-ttu-id="fd776-103">Azure IoT Edge 架構概念</span><span class="sxs-lookup"><span data-stu-id="fd776-103">Azure IoT Edge architectural concepts</span></span>

<span data-ttu-id="fd776-104">檢查任何範例程式碼或使用 IoT Edge 建立專屬現場閘道之前，您應該了解可加強 IoT Edge 架構的重要概念。</span><span class="sxs-lookup"><span data-stu-id="fd776-104">Before you examine any sample code or create your own field gateway using IoT Edge, you should understand the key concepts that underpin the architecture of IoT Edge.</span></span>

## <a name="iot-edge-modules"></a><span data-ttu-id="fd776-105">IoT Edge 模組</span><span class="sxs-lookup"><span data-stu-id="fd776-105">IoT Edge modules</span></span>

<span data-ttu-id="fd776-106">建立和組合「IoT Edge 模組」，即可使用 Azure IoT Edge 來建置閘道。</span><span class="sxs-lookup"><span data-stu-id="fd776-106">You build a gateway with Azure IoT Edge by creating and assembling *IoT Edge modules*.</span></span> <span data-ttu-id="fd776-107">模組使用「訊息」  來彼此交換資料。</span><span class="sxs-lookup"><span data-stu-id="fd776-107">Modules use *messages* to exchange data with each other.</span></span> <span data-ttu-id="fd776-108">模組會接收訊息、對其執行某個動作、選擇性地將其轉換為新的訊息，然後發佈它，以供其他模組處理。</span><span class="sxs-lookup"><span data-stu-id="fd776-108">A module receives a message, performs some action on it, optionally transforms it into a new message, and then publishes it for other modules to process.</span></span> <span data-ttu-id="fd776-109">某些模組可能只會產生新的訊息，且永遠不會處理內送訊息。</span><span class="sxs-lookup"><span data-stu-id="fd776-109">Some modules might only produce new messages and never process incoming messages.</span></span> <span data-ttu-id="fd776-110">一連串的模組可建立資料處理管線，而每個模組都會執行該管線中某個點的資料轉換。</span><span class="sxs-lookup"><span data-stu-id="fd776-110">A chain of modules creates a data processing pipeline with each module performing a transformation on the data at one point in that pipeline.</span></span>

![使用 Azure IoT Edge 所建置之閘道中的模組鏈結][1]

<span data-ttu-id="fd776-112">IoT Edge 包含下列元件：</span><span class="sxs-lookup"><span data-stu-id="fd776-112">IoT Edge contains the following components:</span></span>

* <span data-ttu-id="fd776-113">可執行常見閘道函式的預先撰寫模組。</span><span class="sxs-lookup"><span data-stu-id="fd776-113">Pre-written modules that perform common gateway functions.</span></span>
* <span data-ttu-id="fd776-114">開發人員可用來撰寫自訂模組的介面。</span><span class="sxs-lookup"><span data-stu-id="fd776-114">The interfaces a developer can use to write custom modules.</span></span>
* <span data-ttu-id="fd776-115">部署和執行一組模組所需的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="fd776-115">The infrastructure necessary to deploy and run a set of modules.</span></span>

<span data-ttu-id="fd776-116">SDK 提供一個抽象層，可讓您建置要在各種作業系統和平台上執行的閘道。</span><span class="sxs-lookup"><span data-stu-id="fd776-116">The SDK provides an abstraction layer that enables you to build gateways to run on various operating systems and platforms.</span></span>

![Azure IoT Edge 抽象層][2]

## <a name="messages"></a><span data-ttu-id="fd776-118">訊息</span><span class="sxs-lookup"><span data-stu-id="fd776-118">Messages</span></span>

<span data-ttu-id="fd776-119">雖然考量到彼此傳遞訊息的模組是概念化閘道運作方式的便利方式，但是它不會精確地反映所發生的事情。</span><span class="sxs-lookup"><span data-stu-id="fd776-119">Although thinking about modules passing messages to each other is a convenient way to conceptualize how a gateway functions, it does not accurately reflect what happens.</span></span> <span data-ttu-id="fd776-120">IoT Edge 模組會使用訊息代理程式來互相進行通訊。</span><span class="sxs-lookup"><span data-stu-id="fd776-120">IoT Edge modules use a broker to communicate with each other.</span></span> <span data-ttu-id="fd776-121">模組會將訊息發佈到訊息代理程式 (使用諸如匯流排或發佈/訂閱等傳訊模式)，然後讓訊息代理程式將訊息路由至與它連線的模組。</span><span class="sxs-lookup"><span data-stu-id="fd776-121">Modules publish messages to the broker (using messaging patterns such as bus, or publish/subscribe) and then let the broker route the message to the modules connected to it.</span></span>

<span data-ttu-id="fd776-122">模組使用 **Broker_Publish** 函式將訊息發佈到訊息代理程式。</span><span class="sxs-lookup"><span data-stu-id="fd776-122">A module uses the **Broker_Publish** function to publish a message to the broker.</span></span> <span data-ttu-id="fd776-123">訊息代理程式會叫用回呼函式，以將訊息傳遞到模組。</span><span class="sxs-lookup"><span data-stu-id="fd776-123">The broker delivers messages to a module by invoking a callback function.</span></span> <span data-ttu-id="fd776-124">訊息包含一組索引鍵/值屬性以及傳遞為記憶體區塊的內容。</span><span class="sxs-lookup"><span data-stu-id="fd776-124">A message consists of a set of key/value properties and content passed as a block of memory.</span></span>

![Azure IoT Edge 中的訊息代理程式角色][3]

## <a name="message-routing-and-filtering"></a><span data-ttu-id="fd776-126">訊息路由和篩選</span><span class="sxs-lookup"><span data-stu-id="fd776-126">Message routing and filtering</span></span>

<span data-ttu-id="fd776-127">有兩種方式可將訊息導向正確的 IoT Edge 模組：</span><span class="sxs-lookup"><span data-stu-id="fd776-127">There are two ways to direct messages to the correct IoT Edge modules:</span></span>

* <span data-ttu-id="fd776-128">您可將一組連結傳遞給訊息代理程式，讓訊息代理程式知道每個模組的來源和接收。</span><span class="sxs-lookup"><span data-stu-id="fd776-128">You can pass a set of links can be passed to the broker so the broker knows the source and sink for each module.</span></span>
* <span data-ttu-id="fd776-129">模組可以篩選訊息的屬性。</span><span class="sxs-lookup"><span data-stu-id="fd776-129">A module can filter on the properties of the message.</span></span>

<span data-ttu-id="fd776-130">模組只應對其為適用對象的訊息採取動作。</span><span class="sxs-lookup"><span data-stu-id="fd776-130">A module should only act upon a message if the message is intended for it.</span></span> <span data-ttu-id="fd776-131">連結和訊息篩選可有效地建立訊息管線。</span><span class="sxs-lookup"><span data-stu-id="fd776-131">Links and message filtering effectively create a message pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd776-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fd776-132">Next steps</span></span>

<span data-ttu-id="fd776-133">若要查看這些套用在您可以執行之範例中的概念，請參閱[瀏覽 Azure IoT Edge 架構][lnk-hello-world]。</span><span class="sxs-lookup"><span data-stu-id="fd776-133">To see these concepts applied in a sample you can run, see [Explore Azure IoT Edge architecture][lnk-hello-world].</span></span>

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md