---
title: "aaaIoT 安全性最佳作法 |Microsoft 文件"
description: "保護您 IoT 基礎結構的安全性最佳作法"
services: 
suite: iot-suite
documentationcenter: 
author: YuriDio
manager: timlt
editor: 
ms.assetid: 24e7bda2-5f7b-44e3-b8af-761abd3276ff
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: yurid
ms.openlocfilehash: 3a546c67978a519446ab6c83917a0789675f1b52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-best-practices"></a>物聯網安全性最佳做法
toosecure 物聯網 (IoT) 基礎結構需要嚴格的安全性防禦策略。 此策略需要您 toosecure hello 雲端中的資料、 保護傳輸中的資料完整性超過 hello 公用網際網路，並安全地佈建裝置。 每個圖層建立更大的安全性保證在 hello 整體基礎結構。

## <a name="secure-an-iot-infrastructure"></a>保護 IoT 基礎結構安全
開發和作用中參與的 hello 製造、 開發和部署的 IoT 裝置和基礎結構與相關的各種播放程式來執行這項安全性防禦策略。 以下是這些參與者的高層級說明。  

* **IoT 硬體製造商/積分**： 一般來說，這些是 IoT 硬體正在部署整合者組裝硬體，從各種製造商或供應商提供硬體製造 IoT 部署的 hello 製造商或其他供應商的整合。
* **IoT 方案開發人員**: hello 開發的 IoT 解決方案通常是由方案開發人員。 此開發人員可能是內部團隊的成員，或是專精於此活動的系統整合者 (SI)。 hello IoT 方案開發人員可以開發 hello 從可用的 IoT 解決方案的各種元件、 整合各種現成或開放原始碼的元件，或採用與次要調預先設定的解決方案。
* **IoT 解決方案部署器**： 開發之後的 IoT 解決方案時，它必須 toobe 部署 hello 欄位中。 這牽涉到的硬體，互相連線的裝置，並在硬體裝置或 hello 雲端中的方案部署的部署。
* **IoT 解決方案運算子**: hello 的 IoT 解決方案部署之後，它需要長期作業、 監視、 升級和維護。 這可以包含資訊技術專家、 硬體操作和維護小組和網域專業人員監視正確的行為 hello 整體 IoT 基礎結構的內部團隊所完成。

hello 以下各節提供每個這些玩家 toohelp 的最佳作法開發、 部署和操作安全的 IoT 基礎結構。

## <a name="iot-hardware-manufacturerintegrator"></a>IoT 硬體製造商/整合者
hello hello 最佳作法如下 IoT 硬體製造商和硬體整合者。

* **範圍硬體 toominimum 需求**: hello 硬體設計應該包含 hello 的 hello 硬體，而無其他作業所需的最少的功能。 範例才 tooinclude USB 連接埠的 hello 裝置 hello 操作所需的。 這些額外的功能會開啟，應避免不必要的攻擊誘因的 hello 裝置。
* **進行硬體竄改**： 建置機制 toodetect 實體遭到竄改，例如開啟的 hello 裝置封面或移除 hello 裝置的一部分。 這些修改訊號可能屬於 hello 資料上傳的資料流 toohello 雲端，這可能警示的這些事件的作業。
* **建立周圍安全的硬體**：如果 COGS 允許，請建置安全性功能，例如安全且加密的儲存體，或以信賴平台模組 (TPM) 為基礎的開機功能。 較安全，並協助保護這些功能讓裝置 hello 整體 IoT 基礎結構。
* **進行升級安全**: hello 裝置 hello 存留期間的韌體升級是無法避免。 建置安全路徑升級和密碼編譯保證的軔體版本的裝置可讓 hello 裝置 toobe 安全期間或之後升級。

## <a name="iot-solution-developer"></a>IoT 解決方案開發人員
hello 如下 hello 的 IoT 解決方案開發人員的最佳作法：

* **請遵循安全軟體開發方法**： 開發安全的軟體需要從頭思考安全性、 hello 專案的 hello 從頭所有 hello 方式 tooits 實作、 測試和部署。 所有受影響這個方法與 hello 選擇平台、 語言和工具。 hello Microsoft 安全性開發生命週期提供逐步的方式 toobuilding 安全軟體。
* **選擇小心使用的開放原始碼軟體**： 開放原始碼軟體提供了一個機會 tooquickly 開發方案。 當您選擇的開放原始碼軟體時，請考慮為每個開放原始碼元件的 hello 社群 hello 活動層級。 活躍的社群可確保軟體受到支援，且能發現問題並加以解決。 相反的，隱蔽或不活躍的開放原始碼軟體將不會受到支援，且問題也可能不會被發現。
* **整合小心**： 許多軟體安全性缺陷在於程式庫和應用程式開發介面的 hello 界限。 不需要 hello 目前部署的功能仍然可能透過應用程式開發介面層。 tooensure 整體安全性，請確定 toocheck 元件要整合的安全性是否有缺陷的所有介面。      

## <a name="iot-solution-deployer"></a>IoT 解決方案部署人員
hello 如下的 IoT 解決方案部署器的最佳作法：

* **安全地部署硬體**: IoT 部署可能需要硬體 toobe 部署在不安全的位置，例如公用空間或不受監督的地區設定。 在這種情況下，請確認部署硬體部署防盜 toohello 最大範圍。 在 hello 硬體上使用 USB 或其他通訊埠時，請確定涵蓋方式安全地。 許多攻擊媒介可能會使用這些連接埠做為進入點。
* **維護安全的驗證金鑰**： 在部署期間，每個裝置需要裝置識別碼和相關聯 hello 雲端服務所產生的驗證金鑰。 即使在 hello 部署之後保留這些金鑰實際安全。 惡意裝置 toomasquerade 可以使用任何受危害的金鑰作為現有的裝置。

## <a name="iot-solution-operator"></a>IoT 解決方案操作人員
hello hello 最佳作法如下的 IoT 解決方案運算子：

* **保留 hello 系統，執行 toodate**： 請確定裝置作業系統和所有裝置驅動程式升級的 toohello 最新版本。 如果您開啟自動更新在 Windows 10 （IoT 或其他 Sku），Microsoft 會保留它 toodate，向上 IoT 裝置提供安全的作業系統。 保留其他作業系統 （例如 Linux) 向上 toodate 有助於確保它們也受到惡意的攻擊。
* **防範惡意活動**: hello 作業系統允許時，如果的 hello 最新防毒和反惡意程式碼功能，則會在每個裝置作業系統上安裝。 這有助於減輕大部分的外部威脅。 您可以採取適當步驟，針對威脅來保護大部分的現代化作業系統。
* **經常稽核**： 回應 toosecurity 事件時，安全性相關問題的稽核 IoT 基礎結構是索引鍵。 大部分的作業系統可提供內建事件日誌記錄應該經常檢閱 toomake 確定不發生任何安全性漏洞。 稽核可將資訊傳送為個別的遙測資料流 toohello 雲端服務可以分析它。
* **實際保護 hello IoT 基礎結構**: hello 最差的 IoT 基礎結構的安全性攻擊所使用的實體存取 toodevices 加以啟動。 一個重要的安全作法是 tooprotect 防範惡意的 USB 連接埠及其他實體的存取。 可能發生的一個索引鍵 toouncovering 漏洞記錄的實體存取，例如 USB 連接埠使用。 同樣地，Windows 10 (IoT 和其他 SKU) 可詳細記錄這些事件。
* **保護雲端認證**： 用來設定和操作 IoT 部署的雲端驗證認證可能是最簡單方式 toogain 存取 hello 和入侵 IoT 系統。 經常變更 hello 密碼來保護 hello 認證，並避免公用電腦上使用這些認證。

不同 IoT 裝置的功能會有所差異。 某些裝置可能是執行一般桌面作業系統的電腦，但某些裝置可能會執行非常輕量的作業系統。 先前所述的 hello 安全性最佳作法可能適用 toothese 不同程度的裝置。 如果提供，則應該遵循其他安全性和部署最佳作法從這些裝置的 hello 製造商。

某些舊型和功能受限的裝置可能尚未針對 IoT 部署特別設計。 這些裝置可能會缺少 hello 功能 tooencrypt 資料、 與 hello 網際網路連線，或提供進階稽核。 在這些情況下，新式和安全欄位閘道可以彙總資料，從舊版的裝置，並提供 hello 透過 hello 網際網路連接這些裝置所需的安全性。 欄位閘道可以提供安全驗證、 交涉的加密工作階段、 接收來自 hello 雲端，以及許多其他的安全性功能的命令。

## <a name="see-also"></a>另請參閱
toolearn 有關保護您的 IoT 解決方案的詳細資訊，請參閱：

* [IoT 安全性架構][lnk-security-architecture]
* [保護您的 IoT 部署][lnk-security-deployment]

您也可以探索 hello 的某些其他特性和功能 hello IoT 套件預先設定的解決方案：

* [預先設定的預防性維護解決方案概觀][lnk-predictive-overview]
* [Azure IoT 套件的常見問題集][lnk-faq]

您可以閱讀 IoT 中樞中的安全性[控制存取 tooIoT 中樞][ lnk-devguide-security] hello IoT 中樞開發人員指南 》 中。

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md

[lnk-security-architecture]: iot-security-architecture.md
[lnk-security-deployment]: iot-suite-security-deployment.md
[lnk-devguide-security]: ../iot-hub/iot-hub-devguide-security.md