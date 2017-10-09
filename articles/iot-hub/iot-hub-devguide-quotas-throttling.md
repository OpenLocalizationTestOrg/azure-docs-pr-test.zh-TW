---
title: "aaaUnderstand Azure IoT 中樞配額和節流 |Microsoft 文件"
description: "開發人員指南-hello 配額套用 tooIoT 中樞和 hello 描述預期的節流行為。"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 425e1b08-8789-4377-85f7-c13131fae4ce
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 023fa29bfbfb1de35708d6d121a1c56b50adfed9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-quotas-and-throttling"></a>參考 - IoT 中樞配額和節流

## <a name="quotas-and-throttling"></a>配額和節流
每個 Azure 訂用帳戶最多可以有 10 個 IoT 中樞，以及最多 1 個可用中樞。

每個 IoT 中樞都會以特定 SKU 佈建特定數目的單位 (如需詳細資訊，請參閱 [Azure IoT 中樞定價][lnk-pricing])。 hello SKU 和單位數目決定 hello 每日配額上限的比較，您可以傳送訊息。

hello SKU 也會決定 hello 節流 IoT 中樞會強制執行所有作業的限制。

## <a name="operation-throttles"></a>作業節流
作業節流是速率限制會套用在 hello 分鐘範圍，而且可以預期 tooavoid 濫用。 IoT 中樞嘗試 tooavoid 傳回錯誤，可能的話，但同時也會傳回例外狀況，如果違反 hello 節流的時間太長。

下列表格顯示 hello hello 強制執行節流。 值，請參閱 tooan 個別中樞。

| 節流 | 免費和 S1 中樞 | S2 中樞 | S3 中樞 | 
| -------- | ------- | ------- | ------- |
| 身分識別登錄作業 (建立、擷取、列出、更新、刪除) | 1.67/秒/單位 (100/分鐘/單位) | 1.67/秒/單位 (100/分鐘/單位) | 83.33/秒/單位 (5000/分鐘/單位) |
| 裝置連線 | 最大值為 100/秒或 12/秒/單位 <br/> 例如，兩個 S1 單位是 2\*12 = 24/秒，但是您在所有單位上至少擁有 100/秒。 如果有九個 S1 單位，您的全部單位就會擁有 108/秒 (9\*12)。 | 120/秒/單位 | 6000/秒/單位 |
| 裝置到雲端傳送 | 最大值為 100/秒或 12/秒/單位 <br/> 例如，兩個 S1 單位是 2\*12 = 24/秒，但是您在所有單位上至少擁有 100/秒。 如果有九個 S1 單位，您的全部單位就會擁有 108/秒 (9\*12)。 | 120/秒/單位 | 6000/秒/單位 |
| 雲端到裝置的傳送 | 1.67/秒/單位 (100/分鐘/單位) | 1.67/秒/單位 (100/分鐘/單位) | 83.33/秒/單位 (5000/分鐘/單位) |
| 雲端到裝置的接收 <br/> (僅限裝置使用 HTTP 時)| 16.67/秒/單位 (1000/分鐘/單位) | 16.67/秒/單位 (1000/分鐘/單位) | 833.33/秒/單位 (50000/分鐘/單位) |
| 檔案上傳 | 1.67 檔案上傳通知/秒/單位 (100/分鐘/單位) | 1.67 檔案上傳通知/秒/單位 (100/分鐘/單位) | 83.33 檔案上傳通知/秒/單位 (5000/分鐘/單位) |
| 直接方法 | 20/秒/單位 | 60/秒/單位 | 3000/秒/單位 | 
| 裝置對應項讀取 | 10/秒 | 最大值為 10/秒或 1/秒/單位 | 50/秒/單位 |
| 裝置對應項更新 | 10/秒 | 最大值為 10/秒或 1/秒/單位 | 50/秒/單位 |
| 作業的操作 <br/> (建立、更新、列出、刪除) | 1.67/秒/單位 (100/分鐘/單位) | 1.67/秒/單位 (100/分鐘/單位) | 83.33/秒/單位 (5000/分鐘/單位) |
| 作業的每一裝置操作輸送量 | 10/秒 | 最大值為 10/秒或 1/秒/單位 | 50/秒/單位 |

它是 hello 的重要 tooclarify*裝置連線*節流控制 hello 速率的新裝置可以在建立連線與 IoT 中樞。 hello*裝置連線*節流閥不管理 hello 的同時連線的裝置數目上限。 hello 節流閥 hello 佈建 hello IoT 中樞單位數目而定。

例如，若您購買單一 S1 單位，則得到每秒 100 個連線的節流。 因此，tooconnect 100,000 部裝置，它會採用至少 1000 秒 （約為 16 分鐘）。 不過，若您已將裝置登錄在您的身分識別登錄中，則可以有任意數量的同時連線裝置。

IoT 中樞的深入討論節流行為，請參閱 hello 部落格文章[節流的 IoT 中樞與您][lnk-throttle-blog]。

> [!NOTE]
> 在任何時候，它是可能 tooincrease 配額或節流限制增加 hello 佈建在 IoT 中樞單位數目。
> 
> [!IMPORTANT]
> 身分識別登錄作業是用於裝置管理與佈建案例中的執行階段用途。 透過[匯入和匯出作業][lnk-importexport]，即可支援讀取或更新大量的裝置身分識別。
> 
> 

## <a name="other-limits"></a>其他限制

IoT 中樞會強制執行其他操作限制：

| 作業 | 限制 |
| --------- | ----- |
| 檔案上傳 URI | 10000 個 SAS URI 可以讓儲存體帳戶一次用盡。 <br/> 10 個 SAS URI/裝置可以一次用盡。 |
| 工作 | 作業記錄會保留向上 too30 天 <br/> 並行作業數上限為 1 個 (適用於免費版和 S1)、5 個 (適用於 S2)、10 個 (適用於 S3)。 |
| 額外端點 | 付費 SKU 中樞包含 10 個額外端點。 免費 SKU 中樞包含 1 個額外端點。 |
| 訊息路由規則 | 付費 SKU 中樞包含 100 個路由規則。 免費 SKU 中樞包含 5 個路由規則。 |
| 裝置到雲端傳訊 | 訊息大小上限為 256 KB |
| 雲端到裝置傳訊 | 訊息大小上限為 64 KB |
| 雲端到裝置傳訊 | 擱置傳遞的訊息上限為 50 |

> [!NOTE]
> 目前，hello 最大數目的裝置，您可以連接 tooa 單一 IoT 中樞為 500000。 如果您想 tooincrease 這項限制，請連絡[Microsoft 支援服務](https://azure.microsoft.com/support/options/)。

## <a name="latency"></a>Latency
IoT 中樞會設法 tooprovide 低度延遲的所有作業。 不過，由於 toonetwork 條件和其他因素，無法預測它無法保證最大延遲。 設計您的解決方案時，您應該：

* 請避免進行 hello 最大延遲 IoT 中樞的任何作業的任何假設。
* 佈建您的 IoT 中樞 hello Azure 地區最接近 tooyour 裝置中。
* 請考慮使用 hello 裝置上或在閘道關閉 toohello 裝置上的 Azure IoT 邊緣 tooperform 延遲的作業。

如先前所述，多個 IoT 中樞單位既會影響節流功能，又不會提供額外的延遲好處或保證。
如果您注意到作業的延遲時間莫名其妙增加，請連絡 [Microsoft 支援服務](https://azure.microsoft.com/support/options/)。

## <a name="next-steps"></a>後續步驟
此 IoT 中樞開發人員指南中的其他參考主題包括︰

* [IoT 中樞端點][lnk-devguide-endpoints]
* [裝置對應項、作業和訊息路由的 IoT 中樞查詢語言][lnk-devguide-query]
* [IoT 中樞的 MQTT 支援][lnk-devguide-mqtt]

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[lnk-throttle-blog]: https://azure.microsoft.com/blog/iot-hub-throttling-and-you/
[lnk-importexport]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities

[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
