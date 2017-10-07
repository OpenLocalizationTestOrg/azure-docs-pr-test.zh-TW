---
title: "Microsoft Azure StorSimple 裝置上的 aaaReplace 電池 |Microsoft 文件"
description: "描述如何 tooremove，取代，並維護您的 StorSimple 裝置上的 hello 備用電池模組。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3c8a6654-4826-4883-aad8-75f332347c53
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 542774a5f451ec7ad2bd442f88598df318d8b285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a>取代您的 StorSimple 裝置上的 hello 備用電池模組
## <a name="overview"></a>概觀
hello 主要機箱電源和冷卻模組 (PCM) 在您的 Microsoft Azure StorSimple 裝置上都有額外的電池組。 此組件提供電源，以便 hello StorSimple 裝置可以將資料儲存是否有遺失的 AC 電源 toohello 主要機箱。 這個電池組會參照的 tooas hello*備用電池模組*。 hello 備用電池模組僅存在您的 StorSimple 裝置中的 hello 主要機箱 （hello EBOD 機箱不包含備用電池模組）。 

本教學課程說明如何：

* 移除 hello 備用電池模組 
* 安裝新的備份電池模組
* 維護 hello 備用電池模組

> [!IMPORTANT]
> 移除和更換備用電池模組時，檢閱 hello hello 安全性資訊之前[簡介 tooStorSimple 硬體元件更換](storsimple-hardware-component-replacement.md)。
> 
> 

## <a name="remove-hello-backup-battery-module"></a>移除 hello 備用電池模組
您的 StorSimple 裝置 hello 備用電池模組是欄位置換單元。 它會安裝在 hello PCM 之前，hello 電池模組應存放在其原始包裝。 執行下列步驟 tooremove hello 備用電池的 hello。

#### <a name="tooremove-hello-backup-battery-module"></a>tooremove hello 備用電池模組
1. 在 hello Azure 傳統入口網站中移過**裝置** > **維護** > **硬體狀態**。 在下**共用元件**，查看 hello hello 電池狀態。
2. 識別 hello 中的 hello 電池故障的 PCM。 圖 1 顯示 hello hello StorSimple 裝置背面。
   
    ![裝置主要機箱模組的後擋板](./media/storsimple-battery-replacement/IC740994.png)
   
    **圖 1** 顯示 PCM 和控制器模組的主要裝置背面
   
   | 標籤 | 說明 |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |控制器 0 |
   | 4 |控制器 1 |
   
    Hello 圖 2 中的編號 3 所示，hello 監控指示器 LED 太對應的 PCM 0 上**電池故障**應亮起。
   
    ![裝置後擋板 PCM 監視 LED 指示燈](./media/storsimple-battery-replacement/IC740992.png)
   
    **圖 2**監控指示器 Led 的 PCM 背面顯示 hello
   
   | 標籤 | 說明 |
   |:--- |:--- |
   | 1 |AC 電源故障 |
   | 2 |風扇故障 |
   | 3 |電池故障 |
   | 4 |PCM 正常 |
   | 5 |DC 電源故障 |
   | 6 |電池狀況良好 |
3. tooremove hello PCM 電池故障，請依照下列中的 hello 步驟[移除 PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm)。
4. 已卸下 PCM hello、 增益與 hello 旋轉電池模組向上處理 hello 下列圖表所示，提取 tooremove hello 電池。
   
    ![從 pcm 取出電池](./media/storsimple-battery-replacement/IC741019.png)
   
    **圖 3**正在從 hello PCM hello 電池
5. Hello 模組置於 hello 欄位置換單元封裝。
6. 傳回適當的服務和處理 hello 故障單元 tooMicrosoft。

## <a name="install-a-new-backup-battery-module"></a>安裝新的備份電池模組
執行下列步驟 tooinstall hello 更換電池模組在您的 StorSimple 裝置 hello 主要機箱中的 hello PCM 中的 hello。

#### <a name="tooinstall-hello-battery-module"></a>tooinstall hello 電池模組
1. 將 hello 備用電池模組放在 hello PCM 中的 hello 適當方向。
2. 按向下 hello 電池模組會處理所有的 hello 方式 tooseat hello 連接器。
3. 取代 hello hello 主要機箱中的 PCM，依照下列中的 hello 指導方針[取代您的 StorSimple 裝置上的電源和冷卻模組](storsimple-power-cooling-module-replacement.md)。
4. Hello 更換完成之後，請跳過**裝置** > **維護** > **硬體狀態**hello Azure 傳統入口網站中。 確認 hello hello 電池 toomake 確定 hello 安裝成功狀態。 綠色狀態表示 hello 電池狀況良好。

## <a name="maintain-hello-backup-battery-module"></a>維護 hello 備用電池模組
在您的 StorSimple 裝置 hello 備用電池模組會提供電源 toohello 控制器發生斷電事件期間。 它允許 hello StorSimple 裝置 toosave 重要資料先前 tooshutting 下的以節制的方式。 與 hello Pcm 中兩個完全充電的電池，hello 系統可以處理兩個連續斷電事件。

Hello Azure 傳統入口網站，在 hello**硬體狀態**上 hello**維護**頁面會指出是否 hello 電池無法正常運作或已接近 hello 生命結束。 hello 電池狀態由**PCM 0 中的電池**或**PCM 1 中的電池**下**共用元件**。 此頁面會顯示 [降級] 狀態，表示電池即將用光，以及顯示 [故障]，表示電池已用光。 

> [!NOTE]
> hello 電池可以報告**失敗**只需要支付 toobe 時。
> 
> 

如果 hello**降級**狀態出現，我們建議 hello 之後採取的動作：

* hello 系統發生新的電源中斷或 hello 電池可能正在進行定期維護。 觀察 hello 系統 12 個小時後再繼續。
  
  * 如果 hello 狀態仍**降級**12 小時的持續連接 tooAC 電源以 hello 控制器與 Pcm 執行，然後 hello 之後需要 toobe 更換電池。 請 [連絡 Microsoft 支援](storsimple-contact-microsoft-support.md) ，以取得更換備份電池模組。
  * 如果 hello 後狀態變成 OK 12 小時，hello 電池運作，以及它只需維護費用。
* 如果沒有相關聯的失去 AC 電源和 hello PCM 已開啟且連線 tooAC 電源，需要取代 toobe hello 電池。 [請連絡 Microsoft 支援](storsimple-contact-microsoft-support.md)tooorder 更換備份電池模組。

> [!IMPORTANT]
> 處置 hello 無法根據 toonational 及地區法規的電池。 
> 
> 

## <a name="next-steps"></a>後續步驟
深入了解 [StorSimple 硬體元件更換](storsimple-hardware-component-replacement.md)。

