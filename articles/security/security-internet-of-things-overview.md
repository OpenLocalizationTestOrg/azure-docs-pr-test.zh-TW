---
title: "aaaSecure 您物聯網 (IoT) 在 Azure 中 |Microsoft 文件"
description: " Azure 物聯網 (IoT) 服務提供廣泛的功能。 這篇文章可協助您了解如何 toosecure 您在 Azure 中的 IoT 解決方案。 "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1473c8dd-8669-48fb-86db-b3c50e2eaf59
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: b6cb2ea1c1facada854fb52c55066f34a8289e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-overview"></a>物聯網安全性概觀
Azure 物聯網 (IoT) 服務提供廣泛的功能。 這些企業等級的服務可讓您：

* 從裝置收集資料
* 分析移動中的資料串流
* 儲存和查詢大型資料集
* 視覺化即時和歷程記錄資料
* 與後端辦公室系統整合

toodeliver 一起封裝這些功能，Azure IoT 套件多個 Azure 服務使用自訂延伸模組做為預先設定的解決方案。 這些預先設定的解決方案是常見的 IoT 解決方案模式可協助您採取 toodeliver IoT 解決方案 tooreduce hello 時間的基底實作。 使用 hello IoT 軟體開發套件，您可以自訂及擴充這些解決方案 toomeet 您自己的需求。 您也可以使用這些解決方案作為開發新 IoT 解決方案時的範例或範本。

hello Azure IoT 套件是功能強大的解決方案，針對您的 IoT 需求。 不過，它是您的安全性考量事項從 hello 開始設計的 IoT 解決方案。 Hello 單單只有 IoT 裝置數目，因為任何安全性事件可能很快就會造成嚴重的後果的廣泛事件。

toohelp 您了解如何 toosecure 您的 IoT 解決方案，我們有下列資訊的 hello。

## <a name="security-architecture"></a>安全性架構
在設計系統時，它是重要的 toounderstand hello 潛在威脅 toothat 系統，而且同理，加入適當的措施，因為 hello 系統是設計和架構。 請務必 toodesign 會 hello 的安全性考量事項產品從 hello 開始因為了解如何攻擊者可能會無法 toocompromise 系統可協助確定適當的安全防護處於從 hello 開頭的位置。

您可以了解 IoT 安全性架構，方法是閱讀 [物聯網安全性架構](../iot-suite/iot-security-architecture.md)。

本文將討論下列主題中的 hello:

* [保障安全從威脅模型開始](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [IoT 中的安全性](../iot-suite/iot-security-architecture.md#security-in-iot)
* [威脅模型化 hello Azure IoT 參考架構](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-hello-ground-up"></a>從 hello 接地安全性
hello IoT 帶來唯一的安全性、 隱私權和相容性挑戰 toobusinesses 全球。 與傳統網路技術，其中這些問題心力都圍繞軟體和實作的方式，不同的是 IoT 有關 hello e-security 與 hello 實體領域聚合時會發生什麼事。 保護 IoT 解決方案需要確保安全佈建裝置，這些裝置與 hello 雲端，以及在處理與儲存期間 hello 雲端中的安全資料保護之間的安全連線。 但是，會針對這類功能運作的是資源受限的裝置、根據地理位置分佈的部署，以及解決方案中的許多裝置。

您可以了解如何 toohandle 閱讀這些區域中的安全性[從 hello 地面物聯網安全性](../iot-suite/securing-iot-ground-up.md)。

hello 篇文章會討論下列主題中的 hello:

* [從接地 hello 的安全基礎結構](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [Microsoft Azure - 適用於貴公司的安全 IoT 基礎結構](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a>最佳作法
保護 IoT 基礎結構需要嚴格的深度安全性防禦策略。 從保護 hello 雲端中的資料保護資料的完整性，而傳送 hello 透過公用網際網路，toosecurely 佈建裝置，每個圖層組建中更高的安全性保證 hello 整體基礎結構。

您可以藉由閱讀 [物聯網安全性最佳作法](../iot-suite/iot-security-best-practices.md)，了解物聯網安全性最佳作法。

hello 篇文章會討論下列主題中的 hello:

* [IoT 硬體製造商/整合者](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [IoT 解決方案開發人員](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [IoT 解決方案部署人員](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [IoT 解決方案操作人員](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
