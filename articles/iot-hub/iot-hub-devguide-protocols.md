---
title: "aaaAzure IoT 中樞通訊的通訊協定和連接埠 |Microsoft 文件"
description: "開發人員指南-描述 hello 支援通訊協定裝置到雲端 」 和 「 雲端到裝置的通訊和 hello 必須開啟的連接埠號碼。"
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
ms.openlocfilehash: 31cb948f1d30edd87edb13ad0dd859c02bcc3239
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# 參考 - 選擇通訊協定

IoT 中樞可讓裝置 toouse [MQTT][lnk-mqtt]，透過 WebSockets，MQTT [AMQP][lnk-amqp]，透過 WebSockets 和 HTTP 的 AMQP 通訊協定裝置端通訊。 如需這些通訊協定如何支援特定 IoT 中樞功能的資訊，請參閱[裝置對雲端通訊指引][lnk-d2c-guidance]和[雲端對裝置通訊指引][lnk-c2d-guidance]。

hello 下表提供 hello 高層級的建議您選擇的通訊協定：

| 通訊協定 | 應選擇此通訊協定的情況 |
| --- | --- |
| MQTT <br> 透過 WebSocket 的 MQTT |使用不需要 tooconnect 的所有裝置上多個裝置 （各有自己的每一裝置認證） 透過 hello 相同 TLS 連線。 |
| AMQP <br> 透過 WebSocket 的 AMQP |欄位和雲端閘道 tootake 利用多工在裝置之間的連接上使用。 |
| HTTP |針對無法支援其他通訊協定的裝置使用。 |

請考慮下列點，當您選擇您的裝置後端通訊的通訊協定的 hello:

* **雲端到裝置的模式**。 HTTP 沒有有效的方式 tooimplement 伺服器推入。 因此在使用 HTTP 時，裝置會向 IoT 中樞輪詢雲端到裝置的訊息。 這個方法沒有效率 hello 裝置與 IoT 中樞。 在目前的 HTTP 指導方針中，每個裝置應每隔 25 分鐘或更久進行一次訊息輪詢。 在 hello 另一方面，MQTT 和 AMQP 支援推播接收雲端到裝置訊息時。 它們可讓立即推播通知的訊息從 IoT 中樞 toohello 裝置。 如果傳遞延遲問題，MQTT 或 AMQP 是最佳的通訊協定 toouse hello。 如果是很少連接的裝置，也適用於 HTTP。
* **現場閘道器**。 使用 MQTT 和 HTTP 時，您無法連接多個裝置 （各有自己的每一裝置認證） 使用 hello 相同 TLS 連線。 因此，對於[欄位閘道案例][lnk-azure-gateway-guidance]，這些通訊協定是次佳，因為它們每個裝置連線的 toohello 欄位閘道需要一個 TLS hello 欄位閘道與之間連線的 IoT 中樞。
* **低資源裝置**。 hello MQTT 和 HTTP 程式庫具有較小的耗用量超過 hello AMQP 程式庫。 因此，如果 hello 裝置具有有限的資源 （例如，少於 1 MB RAM），這些通訊協定可能 hello 唯一通訊協定實作使用。
* **網路周遊**。 hello 標準 AMQP 通訊協定使用連接埠 5671、 而 MQTT 接聽通訊埠 8883，都是封閉式的 toonon HTTP 通訊協定的網路中可能會造成問題。 透過 WebSockets MQTT，透過 WebSockets 和 HTTP 的 AMQP 是可用 toobe 本案例中使用。
* **承載大小**。 MQTT 和 AMQP 是二進位通訊協定，這使得其承載比 HTTP 更精簡。

> [!WARNING]
> 使用 HTTP 時，每個裝置應該每隔 25 分鐘或更久輪詢一次雲端到裝置訊息。 不過，在開發期間，它是可接受 toopoll 頻率會比每隔 25 分鐘。

## 連接埠號碼

裝置可以在 Azure 中使用各種通訊協定來與 IoT 中樞通訊。 通常，hello 選擇的通訊協定取決 hello 的 hello 方案的特定需求。 hello 下表列出必須開啟以供裝置 toobe 無法 toouse 特定的通訊協定的 hello 輸出連接埠：

| 通訊協定 | 連接埠 |
| --- | --- |
| MQTT |8883 |
| 透過 WebSocket 的 MQTT |443 |
| AMQP |5671 |
| 透過 WebSocket 的 AMQP |443 |
| HTTP |443 |

一旦您建立 IoT 中樞中的 Azure 區域，hello IoT 中樞會保留 hello 相同的 IP 位址的 IoT 中樞 hello 存留期間。 不過，toomaintain 服務品質，如果 Microsoft 移 hello IoT hub tooa 不同調整規模單位，則會指派新的 IP 位址。


## 後續步驟

toolearn 深入了解如何 IoT 中樞實作 hello MQTT 通訊協定，請參閱[與您使用 hello MQTT 通訊協定的 IoT 中樞通訊][lnk-mqtt-support]。

[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-mqtt-support]: iot-hub-mqtt-support.md
[lnk-amqp]: http://docs.oasis-open.org/amqp/core/v1.0/os/amqp-core-complete-v1.0-os.pdf
[lnk-mqtt]: http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/mqtt-v3.1.1.pdf
[lnk-azure-gateway-guidance]: iot-hub-devguide-endpoints.md#field-gateways
