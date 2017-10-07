---
title: "StorSimple 8000 系列裝置上的 aaaReplace 底座 |Microsoft 文件"
description: "描述如何 tooremove 和取代 hello StorSimple 主要機箱或 EBOD 機箱的底座。"
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
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 94bbd3d354a9b8866ece036238927e67ec5ce2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-chassis-on-your-storsimple-device"></a>取代您的 StorSimple 裝置上的 hello 底座
## <a name="overview"></a>概觀
本教學課程說明如何 tooremove 和取代 StorSimple 8000 系列裝置中的底座。 hello StorSimple 8100 模型是單一機箱裝置 （一個底座），而 hello 8600 是雙重機箱裝置 （兩個底座）。 8600 模型中，有可能兩個底座 hello 裝置中可能會失敗： hello hello 主要機箱的底座或 hello hello EBOD 機箱的底座。

在任一情況下，Microsoft 提供的 hello 取代底座是空的。 將不會包含電源和冷卻模組 (PCM)、控制器模組、固態硬碟 (SSD)、硬碟機 (HDD) 或 EBOD 模組。

> [!IMPORTANT]
> 移除或取代 hello 底座檢閱中的 hello 安全性資訊之前[StorSimple 硬體元件更換](storsimple-8000-hardware-component-replacement.md)。


## <a name="remove-hello-chassis"></a>移除 hello 底座
執行下列步驟 tooremove hello 底座 StorSimple 裝置上的 hello。

#### <a name="tooremove-a-chassis"></a>tooremove 底座
1. 請確定該 hello StorSimple 裝置已關閉，並中斷所有 hello 電源來源。
2. 移除所有 hello 網路和 SAS 纜線，如果適用的話。
3. 移除 hello 機架 hello 單位。
4. 移除每個 hello 磁碟機，並記下移除的 hello 位置。 如需詳細資訊，請參閱[移除 hello 磁碟機](storsimple-8000-disk-drive-replacement.md#remove-the-disk-drive)。
5. 在 hello EBOD 機箱 （如果這是失敗的 hello 底座），移除 hello EBOD 控制器模組。 如需詳細資訊，請參閱 [取下 EBOD 控制器](storsimple-8000-ebod-controller-replacement.md#remove-an-ebod-controller)。
   
    在 hello 主要機箱 （如果這是失敗的 hello 底座），移除 hello 控制站並記下 hello 插槽從中移除。 如需詳細資訊，請參閱 [取下控制器](storsimple-8000-controller-replacement.md#remove-a-controller)。

## <a name="install-hello-chassis"></a>安裝底座 hello
執行下列步驟 tooinstall hello 底座 StorSimple 裝置上的 hello。

#### <a name="tooinstall-a-chassis"></a>tooinstall 底座
1. 掛接 hello 底座 hello 機架中。 如需詳細資訊，請參閱[以機架掛接 StorSimple 8100 裝置](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device)或[以機架掛接 StorSimple 8600 裝置](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device)。
2. Hello 底座 hello 機架中後，請將 hello 控制器模組安裝在相同放置，於先前安裝中的 hello。
3. 安裝 hello 磁碟機的 hello 相同的定位和插槽中，於先前安裝中。
   
   > [!NOTE]
   > 我們建議您首先，安裝 hello Ssd hello 插槽中，然後再安裝 hello Hdd。
  
4. 以 hello hello 機架中掛接裝置和 hello 安裝元件，連接您的裝置 toohello 適當的電源，並開啟 hello 裝置。 如需詳細資料，請參閱[將您的 StorSimple 8100 裝置接上纜線](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device)或[將您的 StorSimple 8600 裝置接上纜線](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device)。

## <a name="next-steps"></a>後續步驟
深入了解 [StorSimple 硬體元件更換](storsimple-8000-hardware-component-replacement.md)。

