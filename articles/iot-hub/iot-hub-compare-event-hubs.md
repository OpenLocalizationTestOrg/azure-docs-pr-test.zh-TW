---
title: "aaaCompare Azure IoT 中樞 tooAzure 事件中心 |Microsoft 文件"
description: "IoT 中樞 hello 和功能差異與使用案例，反白顯示的事件中心的 Azure 服務的比較。 hello 比較包含支援的通訊協定，裝置管理、 監視，並將檔案上傳。"
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: aeddea62-8302-48e2-9aad-c5a0e5f5abe9
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: e5f546b54e29860498d540abfc86a41c4662c0df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-of-azure-iot-hub-and-azure-event-hubs"></a>Azure IoT 中樞和 Azure 事件中樞的比較
IoT 中樞的 hello 主要的使用案例的其中一個是從裝置 toogather 遙測。 基於這個理由，IoT 中樞通常比較太[Azure 事件中心][Azure Event Hubs]。 IoT 中樞，類似事件中心是事件處理服務，可讓事件和遙測 ingress toohello 雲端，同時可靠性高且延遲低的大幅延展。

不過，hello 服務有許多差異，詳述於下表中的 hello:

| 領域 | IoT 中樞 | 事件中樞 |
| --- | --- | --- |
| 通訊模式 | 能夠進行[裝置到雲端通訊][lnk-d2c-guidance] (傳訊、檔案上傳和報告屬性) 和[雲端到裝置通訊][lnk-c2d-guidance] (直接方法、所需屬性、傳訊)。 |僅提供事件輸入 (通常視為裝置到雲端案例)。 |
| 裝置狀態資訊 | [裝置對應項][lnk-twins]可以儲存和查詢裝置狀態資訊。 | 無法儲存裝置狀態資訊。 |
| 裝置通訊協定支援 |支援 MQTT、MQTT over WebSockets、AMQP、AMQP over WebSocket 及 HTTP。 此外，IoT 中樞搭配 hello [Azure IoT 通訊協定閘道][lnk-azure-protocol-gateway]，可自訂的通訊協定閘道實作 toosupport 自訂通訊協定。 |支援 AMQP、透過 WebSockets 的 AMQP 和 HTTP。 |
| 安全性 |提供每個裝置的身分識別與可撤銷的存取控制。 請參閱 hello[安全性 &amp;gt; 一節的 hello IoT 中樞開發人員指南]。 |提供全事件中樞的[共用存取原則][Event Hubs - security]，以及透過[發行者原則][Event Hubs publisher policies]的有限撤銷支援。 IoT 解決方案通常是需要的 tooimplement 自訂方案 toosupport 個別裝置認證和的防詐騙功能的量值。 |
| 作業監視 |可讓 IoT 解決方案 toosubscribe tooa 豐富的裝置身分識別管理和連接事件，例如個別的裝置驗證錯誤、 節流和格式錯誤的例外狀況。 這些事件可讓您 tooquickly 識別 hello 個別的裝置層級的連線問題。 |僅公開彙總的度量。 |
| 調整 |是最佳化的 toosupport 數以百萬計的同時連線的裝置。 |公尺 hello 做為每個連線[Azure 事件中心配額][Azure Event Hubs quotas]。 在 hello 另一方面，事件中心可讓您為每個訊息傳送的 toospecify hello 分割區。 |
| 裝置 SDK |提供[裝置 Sdk] [ Azure IoT SDKs]大型各種不同的平台和語言，加法 toodirect MQTT、 AMQP 和 HTTP 應用程式開發介面中的。 |支援.NET、 Java 和 C，加法 tooAMQP 和 HTTP 傳送介面中。 |
| 檔案上傳 |讓裝置 toohello 雲端的 IoT 解決方案 tooupload 檔案。 包含一個用於整合工作流程的檔案通知端點，以及一個用於支援偵錯的作業監視類別。 | 不支援。 |
| 路由訊息 toomultiple 端點 | 向上 too10 支援自訂端點。 規則會決定訊息的路由的 toocustom 端點的方式。 如需詳細資訊，請參閱[使用 IoT 中樞傳送及接收訊息][lnk-devguide-messaging]。 | 需要額外的程式碼 toobe 寫入，而訊息發送的裝載。 |

總而言之，即使 hello 唯一的使用案例是裝置到雲端遙測 ingress IoT 中樞提供的服務，設計 IoT 裝置連線。 它會繼續 tooexpand hello 價值主張 IoT 特定的功能與這些案例。 事件中心被針對大規模，兩者間資料中心與內部資料中心案例 hello 內容中的事件輸入。

它不是很常見的 toouse IoT 中樞與中的事件中樞 hello 相同的方案。 IoT 中樞處理 hello 裝置到雲端的通訊，而事件中心處理後續階段事件輸入至即時處理引擎。

### <a name="next-steps"></a>後續步驟
toolearn 進一步了解規劃您的 IoT 中樞的部署，請參閱[調整、 高可用性及用為 DR][lnk-scaling]。

toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：

* [IoT 中樞開發人員指南][lnk-devguide]
* [使用 IoT Edge 來模擬裝置][lnk-iotedge]

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[Azure Event Hubs]: ../event-hubs/event-hubs-what-is-event-hubs.md
[安全性 &gt; 一節的 hello IoT 中樞開發人員指南]: iot-hub-devguide-security.md
[Event Hubs - security]: ../event-hubs/event-hubs-authentication-and-security-model-overview.md
[Event Hubs publisher policies]: ../event-hubs/event-hubs-features.md#event-publishers
[Azure Event Hubs quotas]: ../event-hubs/event-hubs-quotas.md
[Azure IoT SDKs]: https://github.com/Azure/azure-iot-sdks
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
