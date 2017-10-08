---
title: "aaaAzure IoT 中樞高可用性和災害復原 |Microsoft 文件"
description: "描述 hello Azure 與 IoT 中樞功能，可協助您 toobuild 高可用性 Azure IoT 解決方案與災害復原功能。"
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: ae320e58-aa20-45b9-abdc-fa4faae8e6dd
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: elioda
ms.openlocfilehash: 74e1fa1682258819ffb3fd84eb79e42fc6e4120f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-high-availability-and-disaster-recovery"></a>IoT 中樞高可用性和災害復原
作為 Azure 服務，IoT 中樞會提供高可用性 (HA) 在 hello Azure 區域層級，使用的備援，而無需 hello 方案所需的任何其他工作。 hello Microsoft Azure 平台也包括功能 toohelp 您建置解決方案，跨區域可用性與災害復原 (DR) 功能。 如果您想 tooprovide 全域，跨地區的裝置或使用者的高可用性設計，並準備您的方案 tootake 利用這些 Azure DR 功能。 hello 文章[Azure 業務續航力技術指引](../resiliency/resiliency-technical-guidance.md)說明 hello 內建功能，在 Azure 中的業務續航力功能和 DR 能力。 hello[災害復原與高可用性 Azure 應用程式][ Disaster recovery and high availability for Azure applications]白皮書提供的架構指引策略 Azure 應用程式 tooachieve HA 功能和 DR 能力。

## <a name="azure-iot-hub-dr"></a>Azure IoT 中樞 DR
此外 toointra 區域 HA IoT 中樞實作嚴重損壞修復的容錯移轉機制，不需要介入 hello 使用者。 IoT 中樞 DR 自我起始，並有 2-26 小時和 hello 下列復原點目標 (Rpo) 的復原時間目標 (RTO)。

| 功能 | RPO |
| --- | --- |
| 登錄和通訊作業的服務可用性 |可能的 CName 遺失 |
| 身分識別登錄中的身分識別資料 |0 到 5 分鐘的資料遺失 |
| 裝置到雲端的訊息 |所有未讀取的訊息都會遺失 |
| 作業監視訊息 |所有未讀取的訊息都會遺失 |
| 雲端到裝置的訊息 |0 到 5 分鐘的資料遺失 |
| 雲端到裝置的意見反應佇列 |所有未讀取的訊息都會遺失 |

## <a name="regional-failover-with-iot-hub"></a>使用 IoT 中心的區域容錯移轉
完整的處理方式的 IoT 解決方案中的部署拓撲超出本文的 hello 範圍。 hello 篇文章討論 hello*地區性容錯移轉*hello 用途的高可用性和災害復原部署模型。

在區域的容錯移轉模式下，hello 方案後端執行主要是在資料中心的位置，而且次要 IoT 中樞及後端部署在另一個資料中心位置。 如果 hello 主要資料中心中的 hello IoT 中樞因發生中斷，或 hello hello 裝置 toohello 主要資料中心的網路連線中斷。 每當無法存取 hello 主要閘道時，裝置會使用次要服務端點。 使用跨地區容錯移轉功能，能夠改善 hello 方案可用性超出單一區域的 hello 高可用性。

在高層級，tooimplement 與 IoT 中樞區域的容錯移轉模型，您需要 hello 下列：

* **次要的 IoT 中樞與路由邏輯裝置**： 在服務中斷，主要區域中的 hello 案例中，裝置必須啟動連接 tooyour 次要區域。 提供的大部分服務相關的 hello 狀態感知本質，通常會方案管理員 tootrigger hello 區域間容錯移轉程序。 hello 最佳方式 toocommunicate hello 新端點 toodevices，同時維持 hello 程序中，控制項是的 toohave 它們定期檢查*指引*hello 目前作用中端點的服務。 hello 指引服務可能是複寫，並保持連線到的 web 應用程式使用 DNS 重新導向技術 (比方說，使用[Azure Traffic Manager][Azure Traffic Manager])。
* **身分識別登錄複寫**-toobe 可用，次要 IoT 中樞 hello 必須包含所有 toohello 方案可以連接到的裝置識別身分。 hello 方案應該保留的裝置識別的異地備援備份，並上傳 toohello 次要 IoT 中樞之後，才能切換 hello hello 裝置的使用中的端點。 hello 裝置身分識別的 IoT 中樞的匯出功能會在此內容中很有用。 如需詳細資訊，請參閱 [IoT 中樞開發人員指南 - 身分識別登錄][IoT Hub developer guide - identity registry]。
* **合併邏輯**-當 hello 主要區域再次變為無法使用，所有 hello 狀態且已建立 hello 次要網站中的資料必須是移轉後 toohello 主要區域。 此狀態與資料大多與相關 toodevice 的身分識別與應用程式中繼資料，必須與 hello 主要 IoT 中樞與 hello 主要區域中的任何其他特定應用程式存放區合併。 toosimplify 此步驟中，您應該使用等冪作業。 作業具有等冪性降到最低 hello 副作用從 hello 最終一致的發佈的事件，以及從重複的項目或次序不對傳遞的事件。 此外，hello 應用程式邏輯應該設計的 tootolerate 潛在的不一致或 「 稍微"結束日期狀態。 這種情況可能是因為 toohello 其他所需的時間 hello 系統太 「 修復 」 根據復原點目標 (RPO)。

## <a name="next-steps"></a>後續步驟
請遵循這些連結 toolearn 深入了解 Azure IoT 中樞：

* [開始使用 IoT 中心 (教學課程)][lnk-get-started]
* [何謂 Azure IoT 中樞？][What is Azure IoT Hub?]

[Disaster recovery and high availability for Azure applications]: ../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md
[Azure Business Continuity Technical Guidance]: https://azure.microsoft.com/documentation/articles/resiliency-technical-guidance/
[Azure Traffic Manager]: https://azure.microsoft.com/documentation/services/traffic-manager/
[IoT Hub developer guide - identity registry]: iot-hub-devguide-identity-registry.md

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[What is Azure IoT Hub?]: iot-hub-what-is-iot-hub.md
