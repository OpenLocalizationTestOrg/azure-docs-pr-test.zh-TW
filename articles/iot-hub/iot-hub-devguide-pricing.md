---
title: "aaaUnderstand Azure IoT 中樞定價 |Microsoft 文件"
description: "開發人員指南 - IoT 中樞計量和計價方式的相關資訊，含實用範例。"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1ac90923-1edf-4134-bbd4-77fee9b68d24
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/12/2016
ms.author: elioda
ms.openlocfilehash: e294c0b7f483e042ca3f63e93c14e0c2d773ae7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-pricing-information"></a>Azure IoT 中樞定價資訊

[Azure IoT 中樞定價][ lnk-pricing]提供不同的 Sku 和價格的 IoT 中樞 hello 一般資訊。 本文章包含如何為計量 IoT 中樞的各種不同功能的 hello 訊息進行 IoT 中樞的其他詳細資料。

## <a name="charges-per-operation"></a>每種作業的費用

| 作業 | 帳單資訊 | 
| --------- | ------------------- |
| 身分識別登錄作業 <br/> (建立、擷取、列出、更新、刪除) | 不收費。 |
| 裝置到雲端的訊息 | 成功傳送的訊息會以輸入至 IoT 中樞的 4 KB 區塊為單位來收費，例如，6 KB 的訊息會收取 2 則訊息的費用。 |
| 雲端到裝置的訊息 | 成功傳送的訊息會以 4 KB 區塊為單位來收費，例如，6 KB 的訊息會收取 2 則訊息的費用。 |
| 檔案上傳 | 檔案傳輸 tooAzure IoT 中樞不計量存放區。 檔案傳輸的啟始和完成訊息會以每 4 KB 的增量方式來就訊息計量收費。 比方說，以便傳輸 10 MB 的檔案會負責在加法 toohello 成本的 Azure 儲存體中的兩個訊息。 |
| 直接方法 | 成功的方法要求會以 4 KB 區塊為單位來收費，具有非空白內文的回應會視為額外的訊息以 4 KB 為單位收費。 要求 toodisconnected 裝置會以 4 KB 區塊 （chunk） 的訊息收費。 比方說，具有 hello 裝置沒有主體之回應中會產生 6 KB 主體的方法會產生費用視為兩則訊息。具有 1 KB 回應 hello 裝置會產生 6 KB 主體的方法會負責為 hello 要求兩個訊息加上另一個 hello 回應訊息。 |
| 裝置對應項讀取 | 裝置的兩個讀取從 hello 的裝置，並從上一步 hello 方案結束時才會收費為 512 位元組的區塊中的訊息。 例如，讀取 6 KB 的裝置對應項會收取 12 則訊息的費用。 |
| 裝置對應項更新 (標籤和屬性) | 裝置 hello 裝置與 hello 裝置的兩個更新會為 512 位元組的區塊中的訊息收費。 例如，讀取 6 KB 的裝置對應項會收取 12 則訊息的費用。 |
| 裝置對應項查詢 | 查詢會為 512 位元組的區塊中的 hello 結果大小而定的訊息收費。 |
| 作業的操作 <br/> (建立、更新、列出、刪除) | 不收費。 |
| 作業的每一裝置操作 | 作業的操作 (例如裝置對應項更新和方法) 會按正常方式收費。 例如，產生 1000 個含 1 KB 要求和空白內文回應之方法呼叫的作業，會收取 1000 則訊息的費用。 |

> [!NOTE]
> 所有大小則會都計算考慮 hello 承載大小，以位元組為單位 （通訊協定框架會被忽略）。 如果訊息 （其中的屬性和內文） hello 大小的計算通訊協定無關的方式，hello 中所述[傳訊開發人員指南的 IoT 中樞][lnk-message-size]。

## <a name="example-1"></a>範例 #1

裝置會傳送一個 1 KB 的裝置到雲端訊息每分鐘 tooIoT 集線器，然後讀取 Azure Stream analytics。 hello 方案後端叫用方法 （具有 512 位元組裝載） hello 裝置上每十分鐘 tootrigger 特定動作。 hello 裝置會回應 200 個位元組的結果 toohello 方法。

hello 裝置消耗 1 則訊息 * 60 分鐘 * 24 小時 = 1440年每天 hello 裝置到雲端訊息，以及 2 要求加上回應的訊息 * 6 次每小時 * 24 小時 = 288 訊息 hello 方法，每日 1728年訊息總數。

## <a name="example-2"></a>範例 2：

某裝置每小時傳送一則 100 KB 的裝置到雲端訊息。 另外，每 4 小時還會以 1KB 的承載更新其裝置對應項。 hello 解決方案回每天一次，結束讀取 hello 14 KB 裝置兩個，並更新它的 512 位元組裝載 toochange 組態。

hello 裝置消耗 25 (100 KB/4 KB) 的訊息 * 24 小時，讓裝置到雲端訊息加上 1 則訊息 * 6 次每天裝置的兩個更新，針對每日 156 訊息總數。
hello 方案後端取用 28 訊息 (14 KB/0.5 KB) tooread hello 裝置兩個，加上 1 訊息 tooupdate 它 29 訊息總數。

總共 hello 裝置和 hello 方案後端取用 185 每天的訊息。


[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[lnk-message-size]: iot-hub-devguide-messages-construct.md
