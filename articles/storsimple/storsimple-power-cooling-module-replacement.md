---
title: "在您的 StorSimple 裝置 PCM aaaReplace |Microsoft 文件"
description: "說明如何 tooremove 和取代 hello 電源和冷卻模組 (PCM) 上您的 StorSimple 裝置"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 24a158cb-0b79-4908-bb5a-431e48760f6a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: cc19ccb29884557720f7538b90dfb05268330b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a>更換 StorSimple 裝置上的電源和冷卻模組
## <a name="overview"></a>概觀
hello 電源和冷卻模組 (PCM) 您的 Microsoft Azure StorSimple 裝置中包含的電源供應器和冷卻風扇控制透過 hello 主要和 EBOD 機箱。 每個機箱只有一個認證的 PCM 模型。 764 W PCM hello 主要機箱已通過認證，而且 hello EBOD 機箱都通過認證 580 W PCM。 雖然主要機箱 hello 和 hello EBOD 機箱的 Pcm hello 不同，但 hello 更換程序是完全相同。

本教學課程說明如何：

* 取下 PCM
* 安裝替代的 PCM

> [!IMPORTANT]
> 移除和更換 PCM，檢閱中的 hello 安全性資訊之前[StorSimple 硬體元件更換](storsimple-hardware-component-replacement.md)。
> 
> 

## <a name="before-you-replace-a-pcm"></a>更換 PCM 之前
請注意下列重要問題，在更換 PCM 之前 hello:

* 如果 hello 電源供應器的 hello PCM 故障，讓 hello 安裝，故障的模組，但移除 hello 電源線。 hello 風扇會繼續 tooreceive hello 機箱電源，並繼續 tooprovide 適當冷卻。 如果 hello 風扇故障，hello PCM 必須立即卸下 toobe。
* 然後再移除 hello PCM，hello 電源中斷 hello PCM，關閉 hello 主開關 （若有的話） 或實際拔 hello 電源線。 這提供警告 tooyour 系統，即將關閉電源。
* 請確定其他 PCM 正常運作的該 hello 繼續系統作業之前取代 hello 故障的 PCM。 必須盡快以可完全正常運作的 PCM 取代故障的 PCM。
* 更換 PCM 模組會採用只有幾分鐘的時間 toocomplete，但它必須移除失敗的 hello PCM tooprevent 過熱的 10 分鐘內完成。
* 請注意 hello 取代 764 W PCM 模組從 hello 原廠出貨不包含 hello 備用電池模組。 您將需要 tooremove hello 電池故障的 PCM，然後再將它插入 hello 取代模組先前 tooperforming hello 更換。 如需詳細資訊，請參閱如何太[移除並插入備份電池模組](storsimple-battery-replacement.md)。

## <a name="remove-a-pcm"></a>取下 PCM
當您準備 tooremove 電源和冷卻模組 (PCM) 從 Microsoft Azure StorSimple 裝置，請遵循這些指示。

> [!NOTE]
> 移除 PCM 之前，請確認您有正確的替換 (764 W 適用於主要機箱 hello) 或 580 W 適用於 hello EBOD 機箱。
> 
> 

#### <a name="tooremove-a-pcm"></a>tooremove PCM
1. 在 hello Azure 傳統入口網站，按一下 **裝置** > **維護** > **硬體狀態**。 檢查 hello hello 之下 PCM 元件狀態**共用元件**tooidentify 哪個 PCM 已故障：
   
   * 如果 PCM 0 中的電源供應器故障，hello 狀態**PCM 0 中的電源供應器**會變成紅色。
   * 如果 PCM 1 中的電源供應器故障，hello 狀態**PCM 1 中的電源供應器**會變成紅色。
   * 如果 PCM 1 中的 hello 風扇故障，hello 狀態中的其中一個**PCM 0 的冷卻 0**或**PCM 0 的冷卻 1**會變成紅色。
2. 找出故障的 PCM 上 hello 回 hello 主要機箱的 hello。 如果您正在 8600 模型，請查看 hello 系統單元識別碼 hello 前端面板 LED 顯示器上顯示識別 hello 主要機箱。 hello 的預設單元識別碼 hello 主要機箱上顯示為**00**，而 hello 預設單元識別碼 hello EBOD 機箱顯示為**01**。 hello 下列圖表說明 hello LED 顯示 hello 前端面板。
   
    ![前置 OPS 面板上的系統識別碼](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     **圖 1** hello 裝置的前面板  
   
   | 標籤 | 說明 |
   |:--- |:--- |
   | 1 |靜音按鈕 |
   | 2 |系統電源 |
   | 3 |模組錯誤 |
   | 4 |邏輯錯誤 |
   | 5 |單元識別碼顯示 |
3. 也可以使用監控指示器 Led hello 主要機箱背面的 hello 中的 hello tooidentify hello 故障的 PCM。 請參閱 hello 下列圖表，以及如何資料表 toounderstand toouse hello Led toolocate hello 故障的 PCM。 例如，如果 hello 導致對應 toohello**風扇故障**會亮起，風扇 hello 已故障。 同樣地，如果 hello 造成太對應**AC 故障**會亮起，hello 電源供應器已故障。 
   
    ![裝置後擋板 PCM 監視 LED 指示燈](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     **圖 2** PCM 背面和 LED 指示燈
   
   | 標籤 | 說明 |
   |:--- |:--- |
   | 1 |AC 電源故障 |
   | 2 |風扇故障 |
   | 3 |電池故障 |
   | 4 |PCM 正常 |
   | 5 |DC 電源故障 |
   | 6 |電池狀況良好 |
4. 請參閱 toohello 遵循 hello hello StorSimple 裝置 toolocate hello 失敗 PCM 模組的背面的圖表。 PCM 0 位於左邊 hello 和 PCM 1 位於右邊 hello。 hello 表會說明 hello 模組。
   
     ![裝置主要機箱模組的後擋板](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     **圖 3** 裝置背面和外掛程式模組 
   
   | 標籤 | 說明 |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |控制器 0 |
   | 4 |控制器 1 |
5. 開啟關閉 hello 故障的 PCM 並中斷連線 hello 電源線。 您現在可以移除 hello PCM。
6. Hello 閂鎖和 hello 側邊的 hello PCM 處理姆指與食指，並將其緊壓在一起的 tooopen hello 控制代碼。
   
    ![開啟 PCM 把手](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    **圖 4**開啟 hello PCM 處理
7. 底框 hello 處理，並移除 hello PCM。
   
    ![取下裝置 PCM](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    **圖 5**移除 hello PCM

## <a name="install-a-replacement-pcm"></a>安裝替代的 PCM
請遵循這些指示 tooinstall StorSimple 裝置中的 PCM。 請確定您已插入 hello 備用電池模組先前 tooinstalling hello 替換 PCM （適用於僅 too764 W Pcm）。 如需詳細資訊，請參閱如何太[移除並插入備份電池模組](storsimple-battery-replacement.md)。

#### <a name="tooinstall-a-pcm"></a>tooinstall PCM
1. 確認您擁有 hello 正確替換 PCM，這個機箱。 hello 主要機箱需要 764 W PCM，而 hello EBOD 機箱則需要 580 W PCM。 您不應嘗試 toouse hello 580 W PCM hello 主要機箱中的或 hello 764 W PCM hello EBOD 機箱中的。 下列影像顯示其中 tooidentify hello 此資訊也就是加上標籤貼附 toohello PCM hello。
   
    ![裝置 PCM 標籤](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    **圖 6** PCM 標籤
2. 檢查有損毀 toohello 機箱，應特別注意 toohello 連接器。 
   
   > [!NOTE]
   > **如果任何連接器插腳，請勿安裝 hello 模組。**
   > 
   > 
3. 以 hello PCM 處理 hello 中開啟投影片 hello hello 機箱模組的位置。
   
    ![安裝裝置 PCM](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    **圖 7**安裝 hello PCM
4. 手動關閉 hello PCM 把手。 您應該為 hello 把手閂鎖嚙合時聽到喀。 
   
   > [!NOTE]
   > hello 的連接器已嚙合，您可以輕輕 tug hello 控制代碼上，但未釋放 hello 閂鎖的 tooensure。 如果 hello PCM 滑出，則表示該 hello 閂鎖 hello 連接器嚙合之前關閉。
   > 
   > 
5. Hello 電源纜線 toohello 電源和 toohello PCM 連接。
6. 浮雕 bales 安全 hello 疲勞。 
7. 開啟 hello PCM。
8. 確認已順利 hello 更換： hello 的 StorSimple Manager 服務的 Azure 傳統入口網站，在瀏覽過**裝置** > **維護** >  **硬體狀態**。 在下**共用元件**，hello 的 hello PCM 的狀態應為綠色。 
   
   > [!NOTE]
   > 可能需要幾分鐘，讓 hello 更換 PCM toocompletely 初始化。
   > 
   > 

## <a name="next-steps"></a>後續步驟
深入了解 [StorSimple 硬體元件更換](storsimple-hardware-component-replacement.md)。

