---
title: "aaaStorSimple 虛擬陣列裝置摘要刀鋒視窗 |Microsoft 文件"
description: "StorSimple 裝置管理員的描述 hello 裝置摘要刀鋒視窗，並說明如何 toouse 它您 StorSimple Virtual Array toomonitor hello 健全狀況。"
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: a13c1ea7-6428-4234-84a6-0ebf51670a85
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: manuaery
ms.openlocfilehash: 3649eaac8a924a772f310a809ddf9706e912157a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-blade-for-storsimple-device-manager-connected-toostorsimple-virtual-array"></a>使用 hello 裝置摘要刀鋒視窗 StorSimple 裝置管理員的連線 tooStorSimple 虛擬陣列

## <a name="overview"></a>概觀

hello StorSimple 裝置管理員裝置刀鋒視窗會提供與給定 StorSimple 裝置管理員 中，註冊 StorSimple Virtual Array 的摘要檢視反白顯示需要系統管理員的注意這些裝置問題。 本教學課程介紹 hello 裝置摘要刀鋒視窗，說明 hello 內容和函式，並說明您可以從這個刀鋒視窗中執行的 hello 工作。

hello 裝置摘要刀鋒視窗會顯示下列資訊的 hello:

![裝置儀表板](./media/storsimple-virtual-array-device-summary/device-blade.png)



## <a name="management"></a>管理

在 hello StorSimple 裝置刀鋒視窗中，您會看到 hello 選項來管理您的 StorSimple 裝置。 您可以看到 hello 的上方 hello 刀鋒視窗和 hello 左邊 hello 管理命令。 使用這些選項 tooadd 共用或磁碟區，或更新，或容錯移轉您的虛擬陣列。

hello essentials 區域擷取部分的 hello 重要屬性，例如，hello 狀態、 模型、 軟體版本，以及連結 toohello **Web UI**的 hello 陣列。 如果您是在內部網路上，您可以直接啟動 hello[本機 web UI](storsimple-ova-web-ui-admin.md) tooadminister 虛擬陣列。

![裝置的基本資訊](./media/storsimple-virtual-array-device-summary/device-essentials.png)

## <a name="storsimple-device-summary"></a>StorSimple 裝置摘要

* hello**警示**磚提供了您的虛擬陣列，依警示嚴重性分組之所有 hello 作用中警示的快照集。 按一下 hello 磚 tooopen hello**警示**刀鋒視窗，然後按一下個別警示 tooview 其他詳細資料的警示，包括任何建議的動作。 如果 hello 問題已經解決，您也可以清除 hello 警示。

* hello**容量**磚顯示 hello 主要儲存體佈建和跨 hello 虛擬裝置相對 toohello 可用總儲存體的剩餘 hello 相同。 **佈建**參考完成準備並配置供使用，儲存體的 toohello 數量**剩餘**參考 toohello 剩餘可以透過此裝置佈建的容量。 hello**剩餘分層**容量是 hello 可以包括雲端，同時 hello 佈建的可用容量**剩餘本機**是 hello 磁碟上剩餘的 hello 容量附加 toothis 虛擬陣列。

* 在 hello**使用量**圖表中，您可以檢視 hello 跨您的虛擬陣列，以及耗用 hello 過去 7 天，hello 預設時間週期的 hello 雲端存放裝置使用的主要儲存體。 使用 hello**編輯**hello 圖表 toochoose hello 右上角中不同的時間間隔的選項。

* hello**共用**或**磁碟區**磚提供的共用或磁碟區，您的裝置依狀態分組中的 hello 數目的摘要。 按一下 hello 磚 tooopen hello**共用**或**磁碟區**清單刀鋒視窗中，然後按一下個別的共用或磁區 tooview 或修改其屬性。 如需詳細資訊，請參閱如何太[管理共用](storsimple-virtual-array-manage-shares.md)或[管理磁碟區](storsimple-virtual-array-manage-volumes.md)。

## <a name="next-steps"></a>後續步驟
了解如何：
- [管理 StorSimple Virtual Array 上的共用](storsimple-virtual-array-manage-shares.md)
    
- [管理 StorSimple Virtual Array 上的磁碟區](storsimple-virtual-array-manage-volumes.md)

