---
title: "aaaAzure IoT 中樞 IP 連線篩選器 |Microsoft 文件"
description: "如何篩選 tooblock 連接從特定 IP 的 toouse IP 位址 tooyour Azure IoT 中樞。 您可以封鎖來自個別 IP 位址或 IP 位址範圍的連接。"
services: iot-hub
documentationcenter: 
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: f833eac3-5b5f-46a7-a47b-f4f6fc927f3f
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: boltean
ms.openlocfilehash: 45e5906a494561b6108895d86d6a04fc3b52b8fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-ip-filters"></a>使用 IP 篩選器

安全性是任何以 Azure IoT 中樞為基礎之 IoT 解決方案的重要一環。 有時候您需要 tooexplicitly hello IP 位址的裝置都能連接指定做為您的安全性組態的一部分。 hello _IP 篩選器_功能可讓您 tooconfigure 規則拒絕或接受來自特定的 IPv4 位址的流量。

## <a name="when-toouse"></a>當 toouse

特定的 IP 位址的有用 tooblock hello IoT 中樞端點時，有兩個特定的使用案例：

- 您的 IoT 中樞只應接收來自指定 IP 位址範圍的流量，並拒絕其他所有流量。 例如，您使用您的 IoT 中樞與[Azure Express Route] toocreate IoT 中樞與您在內部部署基礎結構之間的私人連線。
- 您必須從已經由 hello IoT 中樞管理員識別為可疑的 IP 位址的 tooreject 流量。

## <a name="how-filter-rules-are-applied"></a>篩選器規則的套用方式

hello IP 篩選器規則會套用在 hello IoT 中樞服務層級。 因此 hello IP 篩選器規則適用於 tooall 連線從裝置和使用任何支援的通訊協定的後端應用程式。

嘗試建立連線的 IP 位址若符合 IoT 中樞內的拒絕 IP 規則，將會收到未授權 401 狀態碼和描述。 hello 回應訊息不會提到 hello IP 規則。

## <a name="default-setting"></a>預設設定

根據預設，hello **IP 篩選器**IoT 中樞的 hello 入口網站中的方格是空的。 這項預設設定表示您的中樞可接受來自任何 IP 位址的連線。 這項預設值是對等 tooa 規則可接受 hello 0.0.0.0/0 的 IP 位址範圍。

![IoT 中樞預設 IP 篩選器設定][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a>新增或編輯 IP 篩選器規則

當您新增的 IP 篩選器規則時，系統會提示您 hello 下列值：

- **IP 篩選器規則名稱**必須是唯一、 不區分大小寫英數字元組成 too128 字元字串。 只有 hello ASCII 7 位元英數字元加上`{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}`接受。
- 選取**拒絕**或**接受**為 hello**動作**hello IP 篩選規則。
- 提供單一 IPv4 位址或以 CIDR 標記法表示的 IP 位址區塊。 例如，在 CIDR 標記法 192.168.100.0/22 代表 hello 1024 IPv4 位址從 192.168.100.0 too192.168.103.255。

![新增 IP 篩選器規則 tooan IoT 中樞][img-ip-filter-add-rule]

儲存 hello 規則之後，您會看到警示通知您該 hello 更新正在進行中。

![有關儲存 IP 篩選器規則的通知][img-ip-filter-save-new-rule]

hello**新增**選項已停用，當您到達 hello 最多 10 個 IP 篩選器規則。

按兩下包含 hello 規則的 hello 資料列，您可以編輯現有的規則。

> [!NOTE]
> 拒絕 IP 位址可以防止其他 Azure 服務時 （例如 Azure Stream Analytics、 Azure 虛擬機器或在 hello 入口網站中的 hello 裝置總管） 與 hello IoT 中樞進行互動。

> [!WARNING]
> 如果您使用 Azure 資料流分析 （asa） 一類 tooread 訊息從 IoT 中樞啟用 IP 篩選條件時，使用 hello 事件中樞相容名稱和您的 IoT 中樞端點 hello ASA 連接字串中。

## <a name="delete-an-ip-filter-rule"></a>刪除 IP 篩選器規則

toodelete IP 篩選器規則 hello 方格中按一下 選取一個或多個規則**刪除**。

![刪除 IoT 中樞 IP 篩選器規則][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a>IP 篩選器規則評估

IP 篩選器規則會套用順序並 hello 第一個規則符合 hello IP 位址，會決定 hello 接受或拒絕動作。

例如，如果您想要在 hello 範圍 192.168.100.0/22 tooaccept 位址，並拒絕所有其他項目，hello hello 方格中的第一個規則應該接受 hello 位址範圍 192.168.100.0/22。 hello 下一個規則應該拒絕所有位址使用 hello 範圍 0.0.0.0/0。

您可以變更您的 IP 篩選器規則 hello 方格中的 hello 順序按一下 hello 三個垂直的點在 hello 開頭的資料列並使用拖曳和卸除。

toosave 您新的 IP 篩選器規則的順序，請按一下**儲存**。

![變更您的 IoT 中樞 IP 篩選器規則 hello 順序][img-ip-filter-rule-order]

## <a name="next-steps"></a>後續步驟

toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：

- [作業監視][lnk-monitor]
- [IoT 中樞度量][lnk-metrics]

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
[Azure Express Route]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md