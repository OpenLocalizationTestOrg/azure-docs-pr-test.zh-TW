---
title: "aaaUnderstand Azure IoT 中樞端點 |Microsoft 文件"
description: "開發人員指南 - IoT 中樞裝置對向端點和服務對向端點的相關參考資訊。"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 57ba52ae-19c6-43e4-bc6c-d8a5c2476e95
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 8647f15d2f2a050ad5799ea82f4d2d46db0dbec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-endpoints"></a>參考 - IoT 中樞端點

## <a name="iot-hub-names"></a>IoT 中樞名稱

您可以找到 hello hello IoT 中樞裝載 hello hello 入口網站中的端點名稱**概觀**刀鋒視窗。 根據預設，hello DNS 名稱的 IoT 中樞看起來像： `{your iot hub name}.azure-devices.net`。

您可以使用 Azure DNS toocreate IoT 中樞的自訂 DNS 名稱。 如需詳細資訊，請參閱[一項 Azure 服務使用 Azure DNS tooprovide 自訂網域設定](../dns/dns-custom-domain.md#azure-iot)。

## <a name="list-of-built-in-iot-hub-endpoints"></a>內建 IoT 中樞端點清單

Azure IoT 中樞是公開其功能 toovarious 執行者的多租用戶服務。 hello 下列圖表顯示 hello 各種 IoT 中樞會公開的端點。

![IoT 中樞端點][img-endpoints]

hello 下列清單描述 hello 端點：

* **資源提供者**。 hello IoT 中樞資源提供者會公開[Azure Resource Manager] [ lnk-arm]介面。 此介面可讓 Azure 訂用帳戶擁有者 toocreate，而且刪除 IoT 中樞與 tooupdate IoT 中樞內容。 IoT 中樞屬性用來管理[中樞層級安全性原則][lnk-accesscontrol]，與 toodevice 層級存取控制和雲端到裝置和裝置到雲端訊息的功能選項。 hello IoT 中樞資源提供者也可讓您太[匯出裝置身分識別][lnk-importexport]。
* **裝置身分識別管理**。 每個 IoT 中樞會公開一組 HTTP 的 REST 端點 toomanage 裝置身分識別 （建立、 擷取、 更新和刪除）。 [裝置身分識別][lnk-device-identities]用於裝置驗證和存取控制。
* **裝置對應項管理**。 每個 IoT 中樞會公開一組服務向 HTTP 的 REST 端點 tooquery 和更新[裝置雙][ lnk-twins] （更新標記和屬性）。
* **作業管理**。 每個 IoT 中樞會公開一組服務向 HTTP 的 REST 端點 tooquery 和管理[作業][lnk-jobs]。
* **裝置端點**。 Hello 身分識別登錄中的每個裝置 IoT 中樞會公開一組端點：

  * 傳送裝置到雲端的訊息。 裝置使用此端點太[傳送裝置到雲端訊息][lnk-d2c]。
  * 接收雲端到裝置的訊息。 裝置使用此目標的端點 tooreceive[雲端到裝置訊息][lnk-c2d]。
  * *起始檔案上傳*。 裝置使用此端點 tooreceive 從 IoT 中樞是 Azure 儲存體 SAS URI 太[將檔案上傳][lnk-upload]。
  * *擷取和更新裝置對應項的屬性*。 裝置使用此端點 tooaccess 其[裝置兩個][lnk-twins]的屬性。
  * *接收直接方法要求*。 裝置使用的這個端點 toolisten[直接方法][lnk-methods]的要求。

    公開這些端點時，是使用 [MQTT v3.1.1][lnk-mqtt]、HTTP 1.1 及 [AMQP 1.0][lnk-amqp] 通訊協定來公開。 您也可以透過連接埠 443 上的 [WebSockets][lnk-websockets] 取得 AMQP。

    hello 裝置雙和方法可用的端點只有當您使用 hello 時[MQTT v3.1.1] [ lnk-mqtt]通訊協定。

* **服務端點**。 每個 IoT 中樞以一組您方案的後端 toocommunicate 的端點來公開您的裝置。 有一個例外狀況，這些端點，才會顯示使用 hello [AMQP] [ lnk-amqp]通訊協定。 hello 方法引動過程端點會公開透過 hello HTTP 通訊協定。
  
  * *接收裝置到雲端的訊息*。 此端點與 [Azure 事件中樞][lnk-event-hubs]相容。 後端服務可以使用它 tooread hello[裝置到雲端訊息][ lnk-d2c]您的裝置所傳送。 您可以建立 IoT 中樞上的自訂端點，加法 toothis 內建端點中。
  * *傳送雲端到裝置的訊息及接收傳遞通知*。 這些端點啟用可靠您方案後端 toosend[雲端到裝置訊息][lnk-c2d]，和 tooreceive hello 對應傳遞或逾期的通知。
  * *接收檔案通知*。 此訊息的端點可讓您的 tooreceive 通知時您的裝置已成功上傳的檔案。 
  * *直接方法叫用*。 此端點可讓後端服務 tooinvoke[直接方法][ lnk-methods]在裝置上。
  * *接收作業監視事件*。 此端點可讓您監視的事件，如果您的 IoT 中樞已設定 tooemit tooreceive 作業它們。 如需詳細資訊，請參閱 [IoT 中樞作業監視][lnk-operations-mon]。

hello [Azure IoT Sdk] [ lnk-sdks]文章說明 hello 各種方式 tooaccess 這些端點。

所有的 IoT 中樞端點使用 hello [TLS] [ lnk-tls]未加密/不安全的通道上的通訊協定，以及任何端點曾公開。

## <a name="custom-endpoints"></a>自訂端點

為訊息路由的端點，您可以在訂用帳戶 tooyour IoT 中樞 tooact 連結現有的 Azure 服務。 這些端點可做為服務端點，並當作訊息路由的接收器。 裝置無法直接寫入 toohello 其他端點。 toolearn 進一步了解訊息路由，請參閱 hello 開發人員指南項目上[傳送和接收訊息與 IoT 中樞][lnk-devguide-messaging]。

IoT 中樞目前支援下列其他端點的 Azure 服務的 hello:

* 事件中樞
* 服務匯流排佇列
* 服務匯流排主題

IoT 中樞的訊息路由 toowork 需要寫入權限 toothese 服務端點。 如果您設定透過 hello Azure 入口網站端點，則會為您加入 hello 必要的權限。 請確定您設定您的服務 toosupport hello 預期輸送量。 當您第一次設定您的 IoT 解決方案時，您可能需要 toomonitor 其他端點，並進行必要的調整 hello 實際負載。

如果訊息符合多個路由所有點 toohello 相同的端點，IoT 中樞將傳遞訊息 toothat 端點只有一次。 因此，您不需要 tooconfigure 重複資料刪除服務匯流排佇列或主題上。 在分割佇列中，分割區同質性可保證訊息排序。

> [!NOTE]
> 做為 IoT 中樞端點的服務匯流排佇列和主題不能啟用 [工作階段] 或 [重複偵測]。 如果這些選項的其中一個已啟用，以顯示 hello 端點**連線**hello Azure 入口網站中。

Hello hello 可以新增的端點數目的限制，請參閱[配額和節流][lnk-devguide-quotas]。

## <a name="field-gateways"></a>現場閘道器

在 IoT 解決方案中， *現場閘道*位於裝置和 IoT 中樞端點之間。 它是通常位於關閉 tooyour 裝置。 您的裝置直接與 hello 欄位閘道使用通訊 hello 裝置所支援的通訊協定。 hello 欄位閘道正在連接 tooan IoT 中樞端點使用通訊協定所支援的 IoT 中樞。 現場閘道可能是專用的硬體裝置或是執行自訂閘道軟體的低功率電腦。

您可以使用[Azure IoT 邊緣][ lnk-iot-edge] tooimplement 欄位閘道。 IoT 邊緣提供功能，例如來自 hello 到多個裝置的通訊多工作業相同的 IoT 中樞連線。

## <a name="next-steps"></a>後續步驟

此 IoT 中樞開發人員指南中的其他參考主題包括︰

* [裝置對應項、作業和訊息路由的 IoT 中樞查詢語言][lnk-devguide-query]
* [配額和節流][lnk-devguide-quotas]
* [IoT 中樞的 MQTT 支援][lnk-devguide-mqtt]

[lnk-iot-edge]: https://github.com/Azure/iot-edge

[img-endpoints]: ./media/iot-hub-devguide-endpoints/endpoints.png
[lnk-amqp]: https://www.amqp.org/
[lnk-mqtt]: http://mqtt.org/
[lnk-websockets]: https://tools.ietf.org/html/rfc6455
[lnk-arm]: ../azure-resource-manager/resource-group-overview.md
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/

[lnk-tls]: https://tools.ietf.org/html/rfc5246


[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-accesscontrol]: iot-hub-devguide-security.md#access-control-and-permissions
[lnk-importexport]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-device-identities]: iot-hub-devguide-identity-registry.md
[lnk-upload]: iot-hub-devguide-file-upload.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md

[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[lnk-operations-mon]: iot-hub-operations-monitoring.md
