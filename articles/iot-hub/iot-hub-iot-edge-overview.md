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
# <a name="azure-iot-edge-architectural-concepts"></a>Azure IoT Edge 架構概念

您檢查任何範例程式碼，或建立您自己使用 IoT 邊緣的欄位閘道之前，您應該了解 hello underpin IoT 邊緣 hello 架構的重要概念。

## <a name="iot-edge-modules"></a>IoT Edge 模組

建立和組合「IoT Edge 模組」，即可使用 Azure IoT Edge 來建置閘道。 模組使用*訊息*tooexchange 彼此的資料。 模組接收訊息、 執行一些動作，選擇性地將它轉換成新的訊息，且然後發行它的其他模組 tooprocess。 某些模組可能只會產生新的訊息，且永遠不會處理內送訊息。 模組的鏈結會在一處，該管線中的 hello 資料上執行轉換每個模組建立資料處理管線。

![使用 Azure IoT Edge 所建置之閘道中的模組鏈結][1]

IoT 邊緣包含下列元件的 hello:

* 可執行常見閘道函式的預先撰寫模組。
* hello 介面的開發人員可以使用 toowrite 自訂模組。
* hello 基礎結構需要 toodeploy 和執行模組的設定。

hello SDK 提供一個抽象層，可讓您 toobuild 閘道 toorun 各種作業系統與平台上。

![Azure IoT Edge 抽象層][2]

## <a name="messages"></a>訊息

雖然改善模組傳遞的郵件 tooeach 其他很方便的方式 tooconceptualize 閘道函式，它不會精確地反映會發生什麼事。 IoT 邊緣模組使用 broker toocommunicate 彼此。 模組發佈訊息 toohello broker （使用例如匯流排上，或發行/訂閱傳訊模式），然後讓 hello broker 路由 hello 訊息 toohello 模組連接的 tooit。

模組會使用 hello **Broker_Publish**函式 toopublish 訊息 toohello 代理程式。 hello broker 也會藉由叫用的回呼函式傳遞訊息 tooa 模組。 訊息包含一組索引鍵/值屬性以及傳遞為記憶體區塊的內容。

![hello Broker Azure IoT Edge 中的 hello 角色][3]

## <a name="message-routing-and-filtering"></a>訊息路由和篩選

有兩種方式 toodirect 訊息 toohello 正確 IoT 邊緣模組：

* 您可以將傳遞的一組連結可以傳遞 toohello broker 讓 hello broker 知道 hello 來源和接收的每個模組。
* 模組可以篩選 hello hello 訊息屬性。

如果 hello 訊息用於訊息只應處理模組。 連結和訊息篩選可有效地建立訊息管線。

## <a name="next-steps"></a>後續步驟

請參閱 toosee 套用在範例中，您可以執行這些概念[瀏覽 Azure IoT 邊緣架構][lnk-hello-world]。

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md