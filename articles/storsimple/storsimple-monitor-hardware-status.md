---
title: "aaaStorSimple 硬體元件與狀態 |Microsoft 文件"
description: "了解如何 toomonitor hello hello StorSimple Manager 服務透過 StorSimple 裝置的硬體元件。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 0d56a2ba-daf0-45ad-9610-8b8712dd5750
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: 12a62c0ffc4a5b5e72a25e9e1d976009be03c598
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomonitor-hardware-components-and-status"></a>使用 hello StorSimple Manager 服務 toomonitor 硬體元件和狀態
## <a name="overview"></a>概觀
本文說明 hello 各種實體和邏輯元件在內部部署 StorSimple 裝置中的。 它也會說明 toomonitor 如何使用 hello hello 裝置元件狀態**維護**hello StorSimple Manager 服務中的頁面。 

hello**維護**頁面會顯示所有 hello StorSimple 裝置元件 hello 硬體狀態。 

Hello 8100 的元件清單下有三個區段描述：

* **共用元件**– 這些不屬於 hello 控制站，例如磁碟機、 機箱、 PCM 元件和 PCM 溫度、 線性感應器和線性現階段感應器。
* **控制器 0 元件**– 位於控制器 0，如控制器、 SAS 擴充器和連接器、 控制器溫度感應器，並 hello 各種 hello 元件網路介面。
* **控制器 1 元件**– hello 構成控制器 1，類似 toothose 控制器 0 的詳細的元件。

8600 裝置具有額外對應 toohello 延伸磁碟群 (EBOD) 機箱的元件。 Hello 元件清單下有五個區段。 其中，有三個區段包含 hello 主要機箱中的 hello 元件，而且相同 toohello 8100 所述。 有兩個其他章節 hello EBOD 機箱的：

* **EBOD 機箱共用元件**– hello 元件存在於 hello EBOD 機箱與不屬於 hello EBOD 控制器的 PCM。
* **EBOD 控制器 0 元件**– hello 位於 EBOD 機箱 0，例如 hello EBOD 控制器、 SAS 擴充器和連接器，以及控制器溫度感應器的元件。
* **EBOD 控制器 1 元件**– hello 類似 toothose 詳細 EBOD 機箱 0 的構成 EBOD 機箱 1 的元件。

> [!NOTE]
> **hello 硬體狀態 區段中沒有 hello 維護 頁面上的 StorSimple 虛擬裝置 (1100)。**
> 
> 

## <a name="monitor-hello-hardware-status"></a>監視 hello 硬體狀態
執行下列步驟 tooview hello 硬體裝置元件狀態的 hello:

1. 瀏覽過**裝置**，選取特定的 StorSimple 裝置。 按一下 toogo 於 hello 裝置層級的功能表，然後按一下**維護**。 
2. 找出 hello**硬體狀態**區段，並選擇從 hello 可用的元件 （如上面所述）。 只要按一下箭號前面 hello 元件標籤 tooexpand hello 清單及檢視 hello 狀態 hello 的各種裝置元件。 請參閱 hello [hello 主要機箱的詳細的元件清單](#component-list-for-primary-enclosure-of-storsimple-device)和 hello [hello EBOD 機箱的詳細的元件清單](#component-list-for-ebod-enclosure-of-storsimple-device)。
3. 使用下列的色彩編碼配置 toointerpret hello 元件狀態的 hello:
   
   * **綠色核取符號** – 代表**狀況良好**或**確定**元件。
   * **黃色** – 代表**警告**狀態中的元件。
   * **紅色驚嘆號** – 代表狀態為**失敗**或**需要注意**的元件。
   * **白底黑字** – 代表不存在的元件。
4. 如果您遇到狀態不是「狀況良好」  的元件，請連絡 Microsoft 支援服務。 如果您的裝置上啟用警示，您會收到電子郵件警示。 如果您需要 tooreplace 發生錯誤的硬體元件，請參閱[StorSimple 硬體元件更換](storsimple-hardware-component-replacement.md)。

## <a name="component-list-for-primary-enclosure-of-storsimple-device"></a>StorSimple 裝置之主要機箱的元件清單
hello 表概述 hello hello 在內部部署 StorSimple 裝置的主要機箱中所包含的實體和邏輯元件。

| 元件 | 模組 | 類型 | 位置 | 現場可更換單位 (FRU)？ | 說明 |
| --- | --- | --- | --- | --- | --- |
| 插槽 [0-11] 中的磁碟機 |磁碟機 |實體 |共用 |是 |一條線路為每個 hello SSD 或 hello 主要機箱中的 hello HDD 磁碟機。 |
| 周圍溫度感應器 |機箱 |實體 |共用 |否 |量值 hello hello 底座內的溫度。 |
| 中間板溫度感應器 |機箱 |實體 |共用 |否 |量值 hello hello 中平面的溫度。 |
| 有聲警報器 |機箱 |實體 |共用 |否 |指出 hello 底座內 hello 可發出聲音的警示子系統是否可運作。 |
| 機箱 |機箱 |實體 |共用 |是 |指出底座 hello 存在。 |
| 機箱設定 |機箱 |實體 |共用 |否 |是指 toohello 的 hello 底座的前端面板。 |
| 電源線電壓感應器 |PCM |實體 |共用 |否 |多個線路電壓感應器有顯示其狀態，表示是否 hello 測量的電壓是否在容許範圍內。 |
| 電源線電流感應器 |PCM |實體 |共用 |否 |多個線路電流感應器有顯示其狀態，指出 hello 測量的電流是否在容許範圍內。 |
| PCM 中的溫度感應器 |PCM |實體 |共用 |否 |多個溫度感應器例如入口和作用區感應器有顯示其狀態，指出是否 hello 測量的溫度位於容錯範圍內。 |
| 電源供應器 [0-1] |PCM |實體 |共用 |是 |一條線路為每個在 hello hello 電源供應器位於 hello hello 裝置背面的兩個 Pcm。 |
| 冷卻 [0-1] |PCM |實體 |共用 |是 |一條線路 hello 的每個位於 hello 兩個 Pcm 的四個冷卻風扇。 |
| 電池 [0-1] |PCM |實體 |共用 |是 |一條線路為每個會插入 hello PCM 中的 hello 備用電池模組。 |
| Metis |N/A |邏輯 |共用 |N/A |顯示 hello hello 電池狀態： 是否需要充電，或已接近生命週期結束。 |
| 叢集 |N/A |邏輯 |共用 |N/A |顯示 hello hello 兩個整合式的控制器模組之間建立 hello 叢集狀態。 |
| 叢集節點 |N/A |邏輯 |共用 |N/A |表示 hello 狀態 hello 控制站指定為 hello 叢集的一部分。 |
| 叢集仲裁 |N/A |邏輯 | |N/A |指出 hello 存在 hello HDD 儲存集區中的 hello 多數磁碟成員資格。 |
| HDD 資料空間 |N/A |邏輯 |共用 |N/A |hello 儲存空間用於 hello 硬碟機 (HDD) 儲存集區中的資料。 |
| HDD 管理空間 |N/A |邏輯 |共用 |N/A |hello 空間保留在 hello 管理工作的 HDD 儲存集區。 |
| HDD 仲裁空間 |N/A |邏輯 |共用 |N/A |hello 空間保留在 hello 叢集仲裁的 HDD 儲存集區。 |
| HDD 更換空間 |N/A |邏輯 |共用 |N/A |hello 空間保留在 hello 控制器更換的 HDD 儲存集區。 |
| SSD 資料空間 |N/A |邏輯 |共用 |N/A |hello hello 固態硬碟 (SSD) 儲存集區中的資料所使用的儲存空間。 |
| SSD NVRAM 空間 |N/A |邏輯 |共用 |N/A |hello hello 專用於 NVRAM 邏輯之 SSD 儲存集區中的儲存空間。 |
| HDD 儲存體集區 |N/A |邏輯 |共用 |N/A |顯示 hello 從裝置 Hdd 建立 hello 邏輯儲存集區的狀態。 |
| SSD 儲存體集區 |N/A |邏輯 |共用 |N/A |顯示 hello 從裝置 Ssd 建立 hello 邏輯儲存集區的狀態。 |
| 控制器 [0-1] [狀態] |I/O |實體 |Controller |是 |顯示 hello hello 控制器狀態，以及是否在 hello 底座內的作用中還是待命模式中。 |
| 控制器中的溫度感應器 |I/O |實體 |Controller |否 |例如 I/O 模組、 CPU 溫度、 DIMM 和 PCIe 感應器的多個溫度感應器有顯示其狀態，這表示發生 hello 溫度在容許範圍內。 |
| SAS 擴展器 |I/O |實體 |Controller |否 |表示 hello hello 序列連接 SCSI (SAS) 擴充器，也就是使用的 tooconnect hello 整合式儲存體 toohello 控制器狀態。 |
| SAS 連接器 [0-1] |I/O |實體 |Controller |否 |表示每個 SAS 連接器，也就是使用的 tooconnect 整合式儲存體 toohello SAS 擴充器 hello 狀態。 |
| SBB 中間板相互連接 |I/O |實體 |Controller |否 |表示 hello 中平面連接器，也就是使用的 tooconnect hello 狀態每個控制器 toohello 中平面。 |
| 處理器核心 |I/O |實體 |Controller |否 |表示 hello hello 每個控制器內的處理器核心狀態。 |
| 機箱電子裝置電源 |I/O |實體 |Controller |否 |表示 hello hello 機箱所使用的 hello 電源系統狀態。 |
| 機箱電子裝置診斷 |I/O |實體 |Controller |否 |表示 hello hello 診斷子系統 hello 控制站提供狀態。 |
| 基礎板管理控制器 (BMC) |I/O |實體 |Controller |否 |表示 hello hello 基礎板管理控制器 (BMC)，也就是透過感應器監視 hello 硬體裝置，並與 hello 系統管理員，透過獨立連線通訊的特殊的服務處理器狀態。 |
| 乙太網路 |I/O |實體 |Controller |否 |表示每個 hello 網路介面，也就是 「 hello 管理 」 和 「 hello 控制站上所提供的資料連接埠的 hello 狀態。 |
| NVRAM |I/O |實體 |Controller |否 |指出 hello NVRAM 的狀態，備份 hello 電池的電源故障 hello 事件中提供 tooretain 應用程式關鍵資訊的非揮發性隨機存取記憶體。 |

## <a name="component-list-for-ebod-enclosure-of-storsimple-device"></a>StorSimple 裝置之 EBOD 機箱的元件清單
hello 表概述 hello hello 在內部部署 StorSimple 裝置的 EBOD 機箱中所包含的實體和邏輯元件。

| 元件 | 模組 | 類型 | 位置 | FRU？ | 說明 |
| --- | --- | --- | --- | --- | --- |
| 插槽 [0-11] 中的磁碟機 |磁碟機 |實體 |共用 |是 |一條線路為每個 HDD 磁碟機中 hello hello EBOD 機箱正面的 hello。 |
| 周圍溫度感應器 |機箱 |實體 |共用 |否 |量值 hello hello 底座內的溫度。 |
| 中間板溫度感應器 |機箱 |實體 |共用 |否 |量值 hello hello 中平面的溫度。 |
| 有聲警報器 |機箱 |實體 |共用 |否 |指出 hello 底座內 hello 可發出聲音的警示子系統是否可運作。 |
| 機箱 |機箱 |實體 |共用 |是 |指出底座 hello 存在。 |
| 機箱設定 |機箱 |實體 |共用 |否 |參照 toohello OPS 或 hello 的 hello 底座的前端面板。 |
| 電源線電壓感應器 |PCM |實體 |共用 |否 |多個線路電壓感應器有顯示其狀態，表示是否 hello 測量的電壓是否在容許範圍內。 |
| 電源線電流感應器 |PCM |實體 |共用 |否 |多個線路電流感應器有顯示其狀態，指出 hello 測量的電流是否在容許範圍內。 |
| PCM 中的溫度感應器 |PCM |實體 |共用 |否 |多個溫度感應器例如入口和作用區感應器擁有其狀態顯示，指出是否 hello 測量的溫度位於容錯範圍內。 |
| 電源供應器 [0-1] |PCM |實體 |共用 |是 |一條線路為每個在 hello hello 電源供應器位於 hello hello 裝置背面的兩個 Pcm。 |
| 冷卻 [0-1] |PCM |實體 |共用 |是 |一條線路 hello 的每個位於 hello 兩個 Pcm 的四個冷卻風扇。 |
| 本機儲存體 [HDD] |N/A |邏輯 |共用 |N/A |顯示 hello 從裝置 Hdd 建立 hello 邏輯儲存集區的狀態。 |
| 控制器 [0-1] [狀態] |I/O |實體 |Controller |是 |顯示 hello hello EBOD 模組中的 hello 控制站的狀態。 |
| EBOD 中的溫度感應器 |I/O |實體 |Controller |否 |每一個控制器的多個溫度感應器有顯示其狀態，指出發生 hello 溫度是否在容許範圍內。 |
| SAS 擴展器 |I/O |實體 |Controller |否 |表示 hello hello SAS 擴充器，也就是使用的 tooconnect hello 整合式儲存體 toohello 控制器狀態。 |
| SAS 連接器 [0-2] |I/O |實體 |Controller |否 |表示每個 SAS 連接器，也就是使用的 tooconnect 整合式儲存體 toohello SAS 擴充器 hello 狀態。 |
| SBB 中間板相互連接 |I/O |實體 |Controller |否 |表示 hello 中平面連接器，也就是使用的 tooconnect hello 狀態每個控制器 toohello 中平面。 |
| 機箱電子裝置電源 |I/O |實體 |Controller |否 |表示 hello hello 機箱所使用的 hello 電源系統狀態。 |
| 機箱電子裝置診斷 |I/O |實體 |Controller |否 |表示 hello hello 診斷子系統 hello 控制站提供狀態。 |
| 連接 toodevice 控制器 |I/O |實體 |Controller |否 |表示 hello hello hello I/O EBOD 模組與 hello 裝置控制器之間的連線狀態。 |

## <a name="next-steps"></a>後續步驟
* toouse hello StorSimple Manager 服務 tooadminister 您的裝置，請跳過[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。
* 如果您需要 tootroubleshoot 降級或失敗狀態的裝置元件，請參閱太[StorSimple 監控指示器](storsimple-monitoring-indicators.md)。 
* tooreplace 發生錯誤的硬體元件，請參閱[StorSimple 硬體元件更換](storsimple-hardware-component-replacement.md)。
* 如果您繼續 tooexperience 裝置問題，[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)。

