---
title: "aaaReplace StorSimple EBOD 控制器 |Microsoft 文件"
description: "說明如何 tooremove 和取代 StorSimple 8600 裝置上的一個或兩個 EBOD 控制器。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8cbfa507-1a56-4e24-99dd-7db9abd3b850
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 5d29de2ee30bfdd70910050eee5cfa1d293d444f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a>更換 StorSimple 裝置上的 EBOD 控制器
## <a name="overview"></a>概觀
本教學課程說明如何 tooreplace 上 Microsoft Azure StorSimple 裝置的故障 EBOD 控制器模組。 tooreplace EBOD 控制器模組，您要：

* 移除 hello 故障 EBOD 控制器
* 安裝新的 EBOD 控制器

請考量下列資訊，在您開始前的 hello:

* 空白的 EBOD 模組必須插入至所有未使用的插槽。 如果插槽處於開啟狀態，不會正確地冷卻 hello 機箱。
* hello EBOD 控制器是可熱交換，可移除或取代。 請勿取下故障的模組，除非您有更換模組。 當您起始 hello 更換程序時，您必須在 10 分鐘內完成它。

> [!IMPORTANT]
> 然後再嘗試 tooremove 或取代任何 StorSimple 元件，請確定您檢閱 hello[安全圖示慣例](storsimple-safety.md#safety-icon-conventions)和其他[安全措施](storsimple-safety.md)。
> 
> 

## <a name="remove-an-ebod-controller"></a>取下 EBOD 控制器
取代 hello 失敗 EBOD 控制器模組在您的 StorSimple 裝置，請確定該 hello 其他 EBOD 控制器模組已使用中且正在執行。 hello 下列程序及下表說明如何 tooremove hello EBOD 控制器模組。

#### <a name="tooremove-an-ebod-module"></a>tooremove EBOD 模組
1. 開啟 hello Azure 傳統入口網站。
2. 瀏覽過**裝置** > **維護** > **硬體狀態**，並確認 hello hello 狀態 LED 的 hello active EBOD控制器模組為綠色，而失敗的 hello EBOD 控制器模組的 hello LED 為紅色。
3. 在 hello hello 裝置背面尋找失敗的 hello EBOD 控制器模組。
4. 移除 hello 連接纜線，hello EBOD 控制器模組 toohello 控制器再超出 hello 系統 hello EBOD 模組。
5. 記下 hello 確切 SAS 連接埠已連接的 toohello 控制站的 hello EBOD 控制器模組。 取代 hello EBOD 模組之後，您將會需要的 toorestore hello 系統 toothis 組態。 
   
   > [!NOTE]
   > 一般來說，這將是連接埠 A，標示為**中裝載**hello 下列圖表中。
   > 
   > 
   
    ![EBOD 控制器的後擋板](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     **圖 1** EBOD 模組的背面
   
   | 標籤 | 說明 |
   |:--- |:--- |
   | 1 |故障 LED |
   | 2 |電源 LED |
   | 3 |SAS 連接器 |
   | 4 |SAS LED |
   | 5 |僅供原廠使用的序列埠 |
   | 6 |連接埠 A (主機輸入) |
   | 7 |連接埠 B (主機輸出) |
   | 8 |連接埠 C (僅限原廠使用) |

## <a name="install-a-new-ebod-controller"></a>安裝新的 EBOD 控制器
hello 下列程序及下表說明如何 tooinstall EBOD 控制器模組在您的 StorSimple 裝置。

#### <a name="tooinstall-an-ebod-controller"></a>tooinstall EBOD 控制器
1. 請檢查有無損壞，特別是 toohello 介面連接器 hello EBOD 裝置。 如果有任何彎曲的插腳，請勿安裝 hello 新 EBOD 控制器。
2. Hello 閂鎖在 hello 與開啟投影片 hello hello 閂鎖嚙合之前的 hello 機箱模組的位置。
   
    ![安裝 EBOD 控制器](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    **圖 2**安裝 hello EBOD 控制器模組
3. 關閉 hello 閂鎖。 您應該為 hello 閂鎖嚙合時聽到喀。
   
    ![鬆開 EBOD 閂鎖](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    **圖 3**關閉 hello EBOD 模組閂鎖
4. 重新連線 hello 纜線。 使用 hello hello 更換前出現的確切組態。 請參閱下列圖表中的 hello 和資料表的詳細說明如何 tooconnect hello 纜線。
   
    ![將您的 4U 裝置接上纜線，以取得電源](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    **圖 4**。 重新連接纜線
   
   | 標籤 | 說明 |
   |:--- |:--- |
   | 1 |主要機箱 |
   | 2 |PCM 0 |
   | 3 |PCM 1 |
   | 4 |控制器 0 |
   | 5 |控制器 1 |
   | 6 |EBOD 控制器 0 |
   | 7 |EBOD 控制器 1 |
   | 8 |EBOD 機箱 |
   | 9 |電源分配單元 |

## <a name="next-steps"></a>後續步驟
深入了解 [StorSimple 硬體元件更換](storsimple-hardware-component-replacement.md)。

