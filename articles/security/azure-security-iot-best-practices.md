---
title: "項目安全性最佳做法的 aaaInternet |Microsoft 文件"
description: "hello 發行項提供的項目安全性最佳作法和一般建議的 Microsoft Internet 策劃的清單。"
services: security
documentationcenter: na
author: TomShinder
manager: StevenPo
editor: TomSh
ms.assetid: 2d5598c5-4c30-481d-b8f4-51ee024ea9a7
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: yurid
ms.openlocfilehash: 7ee31c912e8ac230ffa5efcd5b4c2b0b0713584f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-best-practices"></a>物聯網安全性最佳作法
保護的 hello 物聯網 (IoT) 基礎結構是個 IoT 解決方案所需的任何人的重要任務。 由於包含裝置 hello 數目與 hello 分散式的本質，這些裝置，hello 影響安全性事件的相關 toocompromise 數百萬個 IoT 裝置為非一般的而且可以有廣泛的影響。

因此，IoT 安全性需要一套深度安全性作法。 資料需求 toobe 安全 hello 雲端中，因為它會透過私人和公用網路移動。 需要的地方 toosecurely 佈建 hello IoT 裝置本身在 toobe 方法。 每個圖層，從裝置、 toonetwork、 toocloud 後端需要增強式安全性保證。

IoT 最佳作法可以分類在 hello 下列方法：

* IoT 硬體製造商或整合者
* IoT 解決方案開發人員
* IoT 解決方案部署人員
* IoT 解決方案操作人員

本文摘要說明 [物聯網安全性最佳作法](../iot-suite/iot-security-best-practices.md)。 請如需詳細資訊，參閱 toothat 發行項。

## <a name="iot-hardware-manufacturer-or-integrator"></a>IoT 硬體製造商或整合者
如果您是 IoT 硬體製造商或硬體整合器，請遵循 hello 以下的最佳作法：

* **範圍硬體 toominimum 需求**: hello 硬體設計應該包含最少的 hello 硬體，而無其他作業所需的功能。 
* **進行硬體竄改**： 建置機制 toodetect 實體竄改的硬體，例如開啟 hello 裝置封面，移除 hello 裝置等等的一部分。 
* **建立周圍安全的硬體**：如果 [COGS](https://en.wikipedia.org/wiki/Cost_of_goods_sold) 允許，請建立安全性功能，例如以安全與加密儲存體及信任的平台模組 (TPM) 為基礎的開機功能。
* **進行升級安全**: hello 裝置存留期間升級韌體是無可避免的。

## <a name="iot-solution-developer"></a>IoT 解決方案開發人員
如果您的 IoT 解決方案開發人員，請遵循 hello 以下的最佳作法：

* **請遵循安全軟體開發方法**： 開發安全的軟體需要從頭關於 hello 開始 hello 專案的安全性，所有 hello 方式 tooits 實作、 測試和部署。
* **選擇小心使用的開放原始碼軟體**： 開放原始碼軟體提供了一個機會 tooquickly 開發方案。
* **整合小心**： 許多 hello 軟體安全性缺陷在於程式庫和應用程式開發介面的 hello 界限。 

## <a name="iot-solution-deployer"></a>IoT 解決方案部署人員
如果您的 IoT 解決方案部署器，請遵循 hello 以下的最佳作法：

* **安全地部署硬體**: IoT 部署可能需要硬體 toobe 部署在不安全的位置，例如公用空間或不受監督的地區設定。
* **維護安全的驗證金鑰**： 在部署期間，每個裝置需要裝置識別碼和相關聯 hello 雲端服務所產生的驗證金鑰。 即使在 hello 部署之後保留這些金鑰實際安全。 惡意裝置 toomasquerade 可以使用任何受危害的金鑰作為現有的裝置。

## <a name="iot-solution-operator"></a>IoT 解決方案操作人員
如果您的 IoT 解決方案運算子，請遵循 hello 以下的最佳作法：

* **保留系統向上 toodate**： 確保裝置的作業系統和所有裝置驅動程式更新的 toohello 最新版本。 
* **防範惡意活動**: hello 作業系統允許時，如果將 hello 最新的防毒和反惡意程式碼功能放在每個裝置作業系統上。 
* **經常稽核**： 稽核 IoT 基礎結構的安全性相關問題回應 toosecurity 事件時，是索引鍵。
* **實際保護 hello IoT 基礎結構**: hello 最差的 IoT 基礎結構的安全性攻擊所使用的實體存取 toodevices 加以啟動。
* **保護雲端認證**： 用來設定和操作 IoT 部署的雲端驗證認證可能是最簡單方式 toogain 存取 hello 和入侵 IoT 系統。 

