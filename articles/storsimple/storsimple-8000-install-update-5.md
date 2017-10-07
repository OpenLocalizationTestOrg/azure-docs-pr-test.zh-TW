---
title: "StorSimple 8000 系列裝置上的 aaaInstall 更新 5 |Microsoft 文件"
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
ms.date: 08/22/2017
ms.author: alkohli
ms.openlocfilehash: a832f9953e8e39408efeeed375e3afe8eee8d0e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-5-on-your-storsimple-device"></a>在 StorSimple 裝置上安裝 Update 5

## <a name="overview"></a>概觀

本教學課程說明如何在執行較舊的軟體版本，透過 StorSimple 裝置上的更新 5 tooinstall hello Azure 入口網站，並使用 hello hotfix 方法。 不同於 hello StorSimple 裝置的 DATA 0 網路介面上已設定閘道和您嘗試更新前 1 軟體版本從 tooupdate 時使用 hello hotfix 方法。

Update 5 包含裝置軟體、Storport 和 Spaceport、OS 安全性更新和 OS 更新，以及磁碟韌體更新。  hello 裝置軟體、 太空、 Storport、 安全性和其他作業系統更新為非干擾性更新。 透過 hello Azure 入口網站或透過 hello hotfix 方法可以套用 hello 非干擾性或定期更新。 hello 磁碟韌體更新更新具有干擾性，而且會套用 hello 裝置處於維護模式，透過使用 hello 裝置 hello Windows PowerShell 介面 hello hotfix 方法時。

> [!IMPORTANT]
> * 一組預先手動與自動檢查已完成先前 toohello 安裝 toodetermine hello 裝置健全狀況方面硬體狀態和網路連線。 只有當您從 Azure 入口網站 hello 套用 hello 更新時，才執行這些前置檢查。
> * 我們建議您安裝 hello 軟體和其他透過 hello Azure 入口網站的定期更新。 如果 hello 入口網站中的 hello 更新前閘道檢查失敗，應該只會順著 hello 裝置 （tooinstall 更新） toohello Windows PowerShell 介面。 您正在從 hello 版本而定，hello 更新可能需要 4 個小時 （或以上） tooinstall。 hello 維護模式更新必須透過 hello 裝置 hello Windows PowerShell 介面安裝。 由於維護模式更新是干擾性更新，它們會導致裝置的停機時間。
> * 如果執行 hello 選擇性 StorSimple Snapshot Manager，請確定您已升級 Snapshot Manager 版本 tooUpdate 5 先前 tooupdating hello 裝置。


[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-5-via-hello-azure-portal"></a>透過 hello Azure 入口網站安裝更新 5
執行下列步驟 tooupdate hello 裝置太[更新 5](storsimple-update5-release-notes.md)。

> [!NOTE]
> Microsoft 會提取從 hello 裝置的其他診斷資訊。 如此一來，當我們作業小組會識別發生問題的裝置，我們會更好的配備的 toocollect 資訊從裝置 hello 和診斷問題。

[!INCLUDE [storsimple-8000-install-update4-via-portal](../../includes/storsimple-8000-install-update5-via-portal.md)]

確認您的裝置是否正在執行 **StorSimple 8000 系列 Update 5 (6.3.9600.17845)**。 hello**上次更新日期**應該修改。

* 您現在會看見 hello 維護模式更新可供使用 （此訊息可能會繼續顯示總 too24 安裝之後的小時 hello 更新 toobe）。 維護模式更新會導致裝置停機時間，且只能透過您的裝置 hello Windows PowerShell 介面套用干擾性更新。

* 使用 hello 中所列的步驟來下載 hello 維護模式更新[toodownload hotfix](#to-download-hotfixes)如 toosearch 並下載 KB4011837，這會安裝磁碟韌體更新 （hello 其他更新應該已經安裝到目前為止）。 中所列步驟 hello[安裝，並確認 維護模式 hotfix](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello 維護模式更新。

## <a name="install-update-5-as-a-hotfix"></a>以 Hotfix 方式安裝 Update 5


可以使用 hello hotfix 方法來升級的 hello 軟體版本如下：

* Update 0.1、0.2、0.3
* Update 1、1.1、1.2
* Update 2、2.1、2.2
* Update 3、3.1
* Update 4

> [!NOTE] 
> hello 建議方法 tooinstall 更新 5 是透過 hello Azure 入口網站。 如果您無法 hello 閘道核取時，嘗試透過 Azure 入口網站 hello tooinstall hello 更新，請使用此程序。 如果已指派 tooa 非 DATA 0 網路介面閘道和您的裝置正在執行軟體版本更新 1 之前，hello 檢查將會失敗。

hello hotfix 方法牽涉到下列三個步驟的 hello:

1. 從 Microsoft Update 類別目錄 hello 下載 hello hotfix。
2. 安裝並確認 hello 一般模式 hotfix。
3. 安裝並確認 hello 維護模式 hotfix。

#### <a name="download-updates-for-your-device"></a>下載適用於您裝置的更新

您必須下載並安裝 hello 下列 hotfix hello 規定在排序與 hello 建議的資料夾：

| 順序 | KB | 說明 | 更新類型 | 安裝時間 |安裝在資料夾|
| --- | --- | --- | --- | --- | --- |
| 1. |KB4037264 |軟體更新<br> 下載 _HcsSfotwareUpdate.exe_ 和 _CisMSDAgent.exe_ |定期  <br></br>非干擾性 |~ 25 分鐘 |FirstOrderUpdate|

如果從裝置執行 Update 4 的更新，您只需要 tooinstall hello OS 累計更新為第二個訂單的更新。

| 順序 | KB | 說明 | 更新類型 | 安裝時間 |安裝在資料夾|
| --- | --- | --- | --- | --- | --- |
| 2A. |KB4025336 |OS 累積更新套件 <br> 下載 Windows Server 2012 R2 版本 |定期  <br></br>非干擾性 |- |SecondOrderUpdate|

如果從裝置執行 Update 3 安裝或更早版本，安裝 hello 遵循此外 toohello 累計更新。

| 順序 | KB | 說明 | 更新類型 | 安裝時間 |安裝在資料夾|
| --- | --- | --- | --- | --- | --- |
| 2B. |KB4011841 <br> KB4011842 |LSI 驅動程式與韌體更新 <br> USM 韌體更新 (3.38 版) |定期  <br></br>非干擾性 |~ 3 小時 <br> (包括 2A. 2B. + 2C.)|SecondOrderUpdate|
| 2C. |KB3139398 <br> KB3142030 <br> KB3108381 <br> KB3153704 <br> KB3174644 <br> KB3139914   |OS 安全性更新套件 <br> 下載 Windows Server 2012 R2 版本 |定期  <br></br>非干擾性 |- |SecondOrderUpdate|
| 2D. |KB3146621 <br> KB3103616 <br> KB3121261 <br> KB3123538 |OS 更新套件 <br> 下載 Windows Server 2012 R2 版本 |定期  <br></br>非干擾性 |- |SecondOrderUpdate|


您也可能需要在頂端顯示 hello 先前資料表中的所有 hello 更新 tooinstall 磁碟韌體更新。 您可以確認您是否需要執行 hello 來 hello 磁碟韌體更新`Get-HcsFirmwareVersion`cmdlet。 如果您執行這些韌體版本： `XMGJ`， `XGEG`， `KZ50`， `F6C2`， `VR08`， `N003`， `0107`，則您不需要 tooinstall 這些更新。

| 順序 | KB | 說明 | 更新類型 | 安裝時間 | 安裝在資料夾|
| --- | --- | --- | --- | --- | --- |
| 3. |KB4037263 |磁碟韌體 |維護  <br></br>干擾性 |~ 30 分鐘 | ThirdOrderUpdate |

<br></br>

> [!IMPORTANT]
> * 如果更新從更新 4 hello 總計的安裝時間會是關閉 too4 小時。
> * 使用此程序 tooapply hello 前更新，請確定兩個 hello 裝置控制器都在線上，而且所有 hello 硬體元件都均狀況良好。

執行下列步驟 toodownload hello 和安裝 hello hotfix。

[!INCLUDE [storsimple-install-update5-hotfix](../../includes/storsimple-install-update5-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>後續步驟
深入了解 hello[更新 5 release](storsimple-update5-release-notes.md)。

