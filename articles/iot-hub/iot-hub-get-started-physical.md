---
title: "開始連接的實體裝置 tooAzure IoT 中樞 |Microsoft 文件"
description: "深入了解如何 tooconnect 實體裝置和面板 tooAzure IoT 中樞。 您的裝置可以傳送遙測 tooIoT 中樞和 IoT 中心可以監視和管理您的裝置。"
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
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: 47ce289c438b2f495d499d724c38ddc4b3307425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-with-physical-devices-tutorials"></a>Azure IoT 中樞開始使用實體裝置教學課程

這些教學課程介紹 tooAzure IoT 中樞和 hello 裝置 Sdk。 hello 教學課程涵蓋常見 IoT 案例 toodemonstrate hello 功能的 IoT 中樞。 hello 教學課程也說明如何 toocombine IoT 中樞與其他 Azure 服務和工具 toobuild 更強大的 IoT 解決方案。 hello 教學課程中所列 hello 下列表格顯示您如何 toocreate 實體 IoT 裝置。

| IoT 裝置                       | 程式設計語言 |
|---------------------------------|----------------------|
| Raspberry Pi                    | [Python][Pi_Py]、[Node.js][Pi_Nd]、[C][Pi_C]  |
| IoT DevKit                      | [VSCode 中的 Arduino][DevKit]     |
| Intel Edison                    | [Node.js][Ed_Nd]、[C][Ed_C]           |
| Adafruit Feather HUZZAH ESP8266 | [Arduino][Hu_Ard]              |
| Sparkfun ESP8266 Thing 開發人員      | [Arduino][Th_Ard]              |
| Adafruit Feather M0             | [Arduino][M0_Ard]              |

此外，您可以使用 IoT 邊緣閘道 tooenable 裝置 tooconnect tooyour IoT 中樞。

| 閘道裝置               | 程式設計語言 | 平台         |
|------------------------------|----------------------|------------------|
| Intel NUC (模型 DE3815TYKE) | C                    | [Wind River Linux][NUC_Lnx] |

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
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
