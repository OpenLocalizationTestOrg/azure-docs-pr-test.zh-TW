---
title: "aaaAzure IoT 通訊協定閘道 |Microsoft 文件"
description: "如何 toouse Azure IoT 通訊協定閘道 tooextend IoT 中樞功能與通訊協定支援 tooenable 裝置 tooconnect tooyour 集線器使用原本不支援的 IoT 中樞通訊協定。"
services: iot-hub
documentationcenter: 
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 555e59ae-3136-4533-8ba8-f3a3b6acf648
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.openlocfilehash: 9cfed30149672d8f7e021a9899192105bbcdd400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# 讓 IoT 中樞支援其他通訊協定
Azure IoT 中樞原生支援的通訊透過 hello MQTT、 AMQP 和 HTTP 通訊協定。 在某些情況下，裝置或欄位閘道可能無法 toouse 其中一種標準通訊協定，並且需要通訊協定配接。 在這種情況下，您可以使用自訂閘道。 自訂閘道可以啟用 IoT 中樞端點的通訊協定調橋接 hello 流量 tooand 從 IoT 中樞。 您可以使用 hello [Azure IoT 通訊協定閘道](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md)IoT 中樞的自訂閘道 tooenable 通訊協定調整為。

## Azure IoT 通訊協定閘道
hello Azure IoT 通訊協定閘道是一個架構，可供高延展性，雙向裝置與 IoT 中樞通訊的通訊協定配接。 hello 通訊協定閘道是傳遞接受透過特定通訊協定的裝置連線的元件。 它透過 AMQP 1.0 橋接器 hello 流量 tooIoT 中樞。 hello Azure IoT 通訊協定閘道是以使用開放原始碼軟體專案 tooprovide 彈性地加入各種通訊協定與通訊協定版本的支援。

您可以使用 Azure Service Fabric、 Azure 雲端服務背景工作角色或 Windows 虛擬機器，可高度擴充的方式部署在 Azure 中的 hello 通訊協定閘道。 此外，hello 通訊協定閘道可以部署在內部部署環境中，例如欄位的閘道。

hello Azure IoT 通訊協定閘道包含可讓您 toocustomize hello MQTT 通訊協定的行為視 MQTT 通訊協定介面卡。 IoT 中樞 hello MQTT v3.1.1 通訊協定提供內建支援，因為您只應該考慮使用 hello MQTT 通訊協定的配接器，如果不需要通訊協定的自訂或其他功能的特定需求。

hello MQTT 配接器也會示範 hello 程式設計模型，用於建置的其他通訊協定的通訊協定介面卡。 此外，hello Azure IoT 通訊協定閘道程式設計模型可讓您 tooplug 的自訂元件中的特製化處理，例如自訂的驗證、 訊息轉換、 壓縮/解壓縮或加密/解密的流量之間 hello 裝置與 IoT 中樞。

取得彈性，hello 通訊協定閘道 MQTT 實作提供和開放原始碼軟體專案中。 這可讓您視需要 toocustomize hello 實作。

## 後續步驟
深入了解 hello Azure IoT 通訊協定閘道 toolearn 以及 toouse 並將其部署為您的 IoT 解決方案的一部分，請參閱：

* [GitHub 上的 Azure IoT 通訊協定閘道儲存機制 (英文)](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md)
* [Azure IoT 通訊協定閘道開發人員指南 (英文)](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/docs/DeveloperGuide.md)

toolearn 有關規劃您的 IoT 中樞部署的詳細資訊，請參閱：

* [與事件中樞比較][lnk-compare]
* [調整、HA 和 DR][lnk-scaling]
* [IoT 中樞開發人員指南][lnk-devguide]

[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
