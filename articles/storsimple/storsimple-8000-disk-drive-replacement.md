---
title: "aaaReplace StorSimple 8000 系列裝置之磁碟機 |Microsoft 文件"
description: "說明 tooreplace 磁碟 StorSimple 主要機箱或 EBOD 機箱上的磁碟機。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 073/2017
ms.author: alkohli
ms.openlocfilehash: 09c1bf5e97adf54a609a868e921351bc63e00a83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-8000-series-device"></a>更換 StorSimple 8000 系列裝置上的磁碟機

## <a name="overview"></a>概觀
本教學課程說明如何取下和更換 Microsoft Azure StorSimple 裝置上無法運作或故障的硬碟。 tooreplace 磁碟機，您要：

* 卸除 hello 防拆鎖
* 移除 hello 磁碟機
* 安裝 hello 更換磁碟機

> [!IMPORTANT]
> 移除和更換磁碟機，請檢閱中的 hello 安全資訊之前[StorSimple 硬體元件更換](storsimple-8000-hardware-component-replacement.md)。
 

## <a name="disengage-hello-antitamper-lock"></a>卸除 hello 防拆鎖
此程序說明如何 hello StorSimple 裝置上的防拆鎖可以囓合或當您取代 hello 磁碟機。 hello 防拆鎖會納入在 hello 磁碟機托架把手，並透過小孔 hello 控制代碼的 hello 閂鎖區段中存取它們。 Hello 鎖定組 toohello 鎖定位置提供磁碟機。

#### <a name="toounlock-hello-antitamper-lock"></a>toounlock hello 防拆鎖
1. Hello 控制代碼中的 hello 光圈和它的通訊端，小心地將 hello 鎖定鑰匙 （「 防拆 」 T10 螺絲起子 Microsoft 提供）。 
   
   如果已啟動 hello 防拆鎖，hello 紅色指示器中會顯示 hello 光圈。
  
    ![已鎖定磁碟機](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    **圖 1** 防拆鎖已扣上
   
   | 標籤 | 說明 |
   |:--- |:--- |
   | 1 |指示器孔 |
   | 2 |防拆鎖 |
2. 直到 hello 紅色指示器中未顯示 hello 光圈上方 hello 金鑰以逆時針方向旋轉 hello 索引鍵。
3. 移除 hello 索引鍵。
   
    ![已解除鎖定磁碟機](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    **圖 2** 已解除鎖定磁碟機
4. 現在即可卸下 hello 磁碟機。

步驟 hello 反向 tooengage hello 鎖定中。

## <a name="remove-hello-disk-drive"></a>移除 hello 磁碟機
您的 StorSimple 裝置支援如 RAID 10 的儲存空間組態。 這表示它可以在一個磁碟、固態硬碟 (SSD) 或硬碟 (HDD) 故障的情況下正常操作。

> [!IMPORTANT]
> * 如果您的系統有一個以上的故障的磁碟，不要移除一個以上的 SSD 或 HDD hello 系統在任何時間點的時間。 這樣做可能會導致資料遺失。
> * 請確定您將更換 SSD 放置在先前包含 SSD 的插槽中。 同樣地，請將更換 HDD 放置在先前包含 HDD 的插槽中。
> * 在 hello Azure 入口網站，插槽編號為 0 – 11。 因此，如果 hello 入口網站顯示插槽 2 中的磁碟已經失敗，hello 裝置上尋找 hello hello 第三個位置中的故障磁碟從 hello 左上角。
> 
> 

磁碟機可以移除並取代 hello 系統運作時。

#### <a name="tooremove-a-drive"></a>tooremove 磁碟機
1. tooidentify hello 失敗磁碟，請在 hello Azure 入口網站移 tooyour 裝置**設定 > 硬體健全狀況**。 因為磁碟可能會失敗，在 hello 主要機箱和/或 EBOD 機箱 （如果您正使用 8600 模型） 中，查看 hello 狀態下的 hello 磁碟**共用元件**下方和  **EBOD 共用元件**. 任一機箱中故障的磁碟將以紅色狀態顯示。
2. Hello 正面 hello 主要機箱或 hello EBOD 機箱中，找出 hello 磁碟機。 
3. 如果 hello 磁碟已解除鎖定，繼續 toohello 下一個步驟。 如果 hello 磁碟已鎖定，依照下列中的 hello 程序解除鎖定[解除 hello 防拆鎖](#disengage-the-antitamper-lock)。
4. 按 hello 黑色上 hello 磁碟機載具模組閂鎖，而從 hello 底座 hello 前端逾時，立即提取 hello 磁碟機托架把手。
   
    ![鬆開磁碟機把手](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    **圖 3**釋放 hello 磁碟機把手
5. 當 hello 磁碟機托架把手完全延伸，投影片 hello 磁碟機托架超出 hello 底座。 
   
    ![將磁碟滑出磁碟機](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    **圖 4**滑動 hello hello 載波偵測出的磁碟機

## <a name="install-hello-replacement-disk-drive"></a>安裝 hello 更換磁碟機
StorSimple 裝置中故障磁碟機，並將它卸下之後，請遵循此程序 tooreplace 它與新的磁碟機。

#### <a name="tooinsert-a-drive"></a>tooinsert 磁碟機
1. 請確定 hello 磁碟機托架把手完全延伸，hello 下列影像所示。
   
    ![把手已伸展的磁碟機](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    **圖 5** 把手已伸展的磁碟機
2. Hello 所有 hello 方式的磁碟機托架滑入 hello 底座中。
   
    ![將磁碟滑入磁碟機載具](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    **圖 6**滑動 hello 磁碟機托架至 hello 底座
3. 與 hello 磁碟機托架插入，請關閉 hello 磁碟機托架把手時繼續 toopush hello 磁碟機托架至 hello 底座，直到 hello 磁碟機托架把手扣入鎖定的位置。
4. 由 Microsoft （防拆 Torx 螺絲起子） toosecure hello 托架把手位置提供藉由開啟 hello 鎖定螺絲四分之一順時針使用 hello lock 鍵。
5. 請確認 hello 更換成功，而且 hello 磁碟機可運作。 存取 hello Azure 入口網站並瀏覽過**設定** > **硬體健全狀況**。 在下**共用元件**或**EBOD 共用元件**，hello 磁碟機狀態應為綠色，表示運作正常。
<!---Loc Comment: It seems it should say "Device settings > Hardware health" instead of "Settings > Hardware health"---->
   
   > [!NOTE]
   > 它可能需要幾個小時 hello 磁碟狀態 tooturn 綠色之後 hello 取代。
  
## <a name="next-steps"></a>後續步驟
深入了解 [StorSimple 硬體元件更換](storsimple-8000-hardware-component-replacement.md)。

