---
title: "在您的 StorSimple 裝置上的 Update 4 aaaInstall |Microsoft 文件"
description: "說明如何在您的 StorSimple 8000 系列裝置 tooinstall StorSimple 8000 系列 Update 4。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/30/2017
ms.author: alkohli
ms.openlocfilehash: 62c0ae94afdbb1027d3075962afa04d49fd1f60a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-4-on-your-storsimple-device"></a>在 StorSimple 裝置上安裝 Update 4

## <a name="overview"></a>概觀

本教學課程說明如何在執行較舊的軟體版本，透過 StorSimple 裝置上的 tooinstall Update 4 hello Azure 傳統入口網站，並使用 hello hotfix 方法。 不同於 hello StorSimple 裝置的 DATA 0 網路介面上已設定閘道和您嘗試更新前 1 軟體版本從 tooupdate 時使用 hello hotfix 方法。

Update 4 包含裝置軟體、USM 韌體、LSI 驅動程式與韌體、Storport 和 Spaceport、OS 安全性更新和許多其他作業系統更新。  hello 裝置軟體、 USM 韌體、 太空、 Storport 和其他作業系統更新為非干擾性更新。 透過 hello Azure 傳統入口網站或透過 hello hotfix 方法可以套用 hello 非干擾性或定期更新。 hello 磁碟韌體更新更新具有干擾性，並只能透過 hello hotfix 方法使用 hello 裝置 hello Windows PowerShell 介面套用。 

> [!IMPORTANT]
> * 一組預先手動與自動檢查已完成先前 toohello 安裝 toodetermine hello 裝置健全狀況方面硬體狀態和網路連線。 只有當您從 Azure 傳統入口網站 hello 套用 hello 更新時，才執行這些前置檢查。
> * 我們建議您安裝 hello 軟體和其他透過 hello Azure 傳統入口網站的定期更新。 如果 hello 入口網站中的 hello 更新前閘道檢查失敗，應該只會順著 hello 裝置 （tooinstall 更新） toohello Windows PowerShell 介面。 您正在從 hello 版本而定，hello 更新可能需要 4 個小時 （或以上） tooinstall。 hello 維護模式更新也必須安裝透過 hello 裝置 hello Windows PowerShell 介面。 由於維護模式更新是干擾性更新，它們將會導致裝置的停機時間。
> * 如果執行 hello 選擇性 StorSimple Snapshot Manager，請確定您已升級 Snapshot Manager 版本 tooUpdate 4 先前 tooupdating hello 裝置。


[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-4-via-hello-azure-classic-portal"></a>安裝更新 4 透過 hello Azure 傳統入口網站
執行下列步驟 tooupdate hello 裝置太[Update 4](storsimple-update4-release-notes.md)。

> [!NOTE]
> 如果您要套用 Update 2 或更新版本 （包括 Update 2.1)，Microsoft 將會無法 toopull 其他診斷的資訊從裝置 hello。 如此一來，當我們作業小組會識別發生問題的裝置，我們會更好的配備的 toocollect 資訊從裝置 hello 和診斷問題。 接受更新 2 或更新版本，您允許我們 tooprovide 主動式這項支援。 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

確認您的裝置是否正在執行 **StorSimple 8000 系列 Update 4 (6.3.9600.17820)**。 hello**上次更新日期**也應修改。 

* 您現在會看見 hello 維護模式更新可供使用 （此訊息可能會繼續顯示總 too24 安裝之後的小時 hello 更新 toobe）。 維護模式更新會導致裝置停機時間，且只能透過您的裝置 hello Windows PowerShell 介面套用干擾性更新。
 
* 使用 hello 中所列的步驟來下載 hello 維護模式更新[toodownload hotfix](#to-download-hotfixes)如 toosearch 並下載 KB4011837，這會安裝磁碟韌體更新 （hello 其他更新應該已經安裝到目前為止）。 中所列步驟 hello[安裝，並確認 維護模式 hotfix](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello 維護模式更新。 

## <a name="install-update-4-as-a-hotfix"></a>以 Hotfix 方式安裝 Update 4
hello 建議方法 tooinstall Update 4 是透過 hello Azure 傳統入口網站。

如果您無法 hello 閘道核取時，嘗試透過 hello Azure 傳統入口網站的 tooinstall hello 更新，請使用此程序。 hello 檢查失敗，因為您已指派 tooa 非 DATA 0 網路介面閘道和您的裝置正在執行軟體版本先前 tooUpdate 1。

可以使用 hello hotfix 方法來升級的 hello 軟體版本如下：

* Update 0.1、0.2、0.3
* Update 1、1.1、1.2
* Update 2、2.1、2.2
* Update 3、3.1 


hello hotfix 方法牽涉到下列三個步驟的 hello:

1. 從 Microsoft Update 類別目錄 hello 下載 hello hotfix。
2. 安裝並確認 hello 一般模式 hotfix。
3. 安裝並確認 hello 維護模式 hotfix。

#### <a name="download-updates-for-your-device"></a>下載適用於您裝置的更新

您必須下載並安裝 hello 下列 hotfix hello 規定在排序與 hello 建議的資料夾：

| 順序 | KB | 說明 | 更新類型 | 安裝時間 |安裝在資料夾|
| --- | --- | --- | --- | --- | --- |
| 1. |KB4011839 <br> (2 個檔案) |裝置軟體更新 <br> CiS/MDS 代理程式更新 |定期 <br></br>非干擾性 |~ 25 分鐘 |FirstOrderUpdate <br> _先安裝裝置軟體更新再安裝 Cis/MDS 代理程式更新_|
| 2A. |KB4011841 <br> KB4011842 |LSI 驅動程式與韌體更新 <br> USM 韌體更新 (3.38 版) |定期  <br></br>非干擾性 |~ 3 小時 <br> (包括 2A. 2B. + 2C.)|SecondOrderUpdate|
| 2B. |KB3139398、KB3108381 <br> KB3205400、KB3142030 <br> KB3197873、KB3192392  <br> KB3153704、KB3174644 <br> KB3139914  |OS 安全性更新套件 |定期  <br></br>非干擾性 |- |SecondOrderUpdate|
| 2C. |KB3210083、KB3103616 <br> KB3146621、KB3121261 <br> KB3123538 |OS 更新套件 |定期  <br></br>非干擾性 |- |SecondOrderUpdate|

您也可能需要在頂端顯示 hello 先前資料表中的所有 hello 更新 tooinstall 磁碟韌體更新。 您可以確認您是否需要執行 hello 來 hello 磁碟韌體更新`Get-HcsFirmwareVersion`cmdlet。 如果您執行這些韌體版本： `XMGJ`， `XGEG`， `KZ50`， `F6C2`， `VR08`， `N002`， `0106`，則您不需要 tooinstall 這些更新。

| 順序 | KB | 說明 | 更新類型 | 安裝時間 | 安裝在資料夾|
| --- | --- | --- | --- | --- | --- |
| 3. |KB4011837 |磁碟韌體 |維護  <br></br>干擾性 |~ 30 分鐘 | ThirdOrderUpdate |

<br></br>

> [!IMPORTANT]
> * 此程序需求 toobe 只能執行一次 tooapply Update 4。 您可以使用 hello Azure 傳統入口網站 tooapply 後續更新。
> * 如果從 Update 3 或 3.1 版的更新，hello 總計的安裝時間將會是關閉 too4 小時。
> * 使用此程序 tooapply hello 前更新，請確定兩個 hello 裝置控制器都在線上，而且所有 hello 硬體元件都均狀況良好。

執行下列步驟 toodownload hello 和安裝 hello hotfix。

[!INCLUDE [storsimple-install-update4-hotfix](../../includes/storsimple-install-update4-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>後續步驟
深入了解 hello [Update 4 版本](storsimple-update4-release-notes.md)。

