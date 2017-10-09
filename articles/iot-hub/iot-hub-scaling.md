---
title: "aaaAzure IoT 中樞調整 |Microsoft 文件"
description: "如何 tooscale 您的 IoT 中樞 toosupport 預期的訊息輸送量。 包含摘要的 hello 支援的每一層的輸送量與分區化的選項。"
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: e7bd4968-db46-46cf-865d-9c944f683832
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3b8bf6c44631c65b34b69752d9043c21db24bb01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-iot-hub-solution"></a>調整您的 IoT 中樞解決方案
Azure IoT 中樞可以支援 tooa 百萬個同時連接的裝置註冊。 如需詳細資訊，請參閱 [IoT 中樞價格][lnk-pricing]。 每個 IoT 中樞單位允許一定數量的每日訊息。

tooproperly 調整您的方案，請考慮您的 IoT 中樞的特殊使用。 特別是，請考慮下列的作業類別目錄的 hello 的所需的 hello 尖峰輸送量：

* 裝置到雲端的訊息
* 雲端到裝置的訊息
* 身分識別登錄作業

在其他 toothis 輸送量資訊，請參閱[IoT 中樞配額與節流閥][ IoT Hub quotas and throttles]並據此設計您的方案。

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a>裝置到雲端及雲端到裝置訊息輸送量
最佳的方式 toosize hello IoT 中樞方案是以每單位為基礎的 tooevaluate hello 流量。

裝置到雲端訊息會遵循這些持續的輸送量指導方針。

| 層 | 持續的輸送量 | 持續的傳送速率 |
| --- | --- | --- |
| S1 |向上 too1111 KB/每單位分鐘<br/>(1.5 GB/天/單位) |每個單位平均 278 個訊息/分鐘<br/>(400,000 個訊息/天/單位) |
| S2 |向上 too16 MB/每單位分鐘<br/>(22.8 GB/天/單位) |每個單位平均 4,167 個訊息/分鐘<br/>(600 萬個訊息/天/單位) |
| S3 |向上 too814 MB/每單位分鐘<br/>(1144.4 GB/天/單位) |每個單位平均 208,333 個訊息/分鐘<br/>(3 億個訊息/天/單位) |

## <a name="identity-registry-operation-throughput"></a>身分識別登錄作業輸送量
IoT 中樞身分登錄作業不應 toobe 執行階段作業，因為它們通常是相關的 toodevice 佈建。

對於明顯暴增的效能數據，請參閱 [IoT 中樞配額和節流][IoT Hub quotas and throttles]。

## <a name="sharding"></a>分區化
雖然單一的 IoT 中樞可以調整 toomillions 的裝置，有時候您的方案需要特定的效能特性，單一的 IoT 中樞無法保證。 在此情況下，建議您將裝置分割成多個 IoT 中樞。 多個 IoT 中樞 smooth 流量暴增，並取得 hello 必要的輸送量或所需的作業速率。

## <a name="next-steps"></a>後續步驟
toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：

* [IoT 中樞開發人員指南][lnk-devguide]
* [使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
