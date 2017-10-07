---
title: "aaaStorSimple 虛擬陣列更新 0.4 版本資訊 |Microsoft 文件"
description: "描述重要開啟問題和解決 hello StorSimple Virtual Array 執行更新 0.4。"
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
ms.workload: NA
ms.date: 04/05/2017
ms.author: alkohli
ms.openlocfilehash: 1fd174ff483f4f7b1b4a7853c9d9573d1e948cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-04-release-notes"></a>StorSimple Virtual Array Update 0.4 版本資訊

## <a name="overview"></a>概觀

hello 下列版本資訊找出 hello 重大開啟問題並 hello 更新 Microsoft Azure StorSimple Virtual Array 已解決的問題。

hello 版本資訊會持續更新，並在發現需要因應措施的重大問題時，會加入。 部署 StorSimple 虛擬陣列之前，請仔細檢閱 hello hello 版本資訊中所包含的資訊。

更新 0.4 對應 toohello 軟體版本**10.0.10289.0**。

> [!NOTE]
> 更新是干擾性作業，會重新啟動您的裝置。 如果正在進行中的 I/O，hello 裝置會產生停機時間。


## <a name="whats-new-in-hello-update-04"></a>新功能更新 0.4 hello
Update 0.4 是主要的錯誤修正組建，而且包含一些加強功能。 在此版本中，導致備份失敗 hello 前一版中的數個 bug 已解決。 hello 主要增強功能和 bug 修正如下：

- **備份效能增強功能**-此版本中進行了幾個索引鍵增強功能 tooimprove hello 備份效能。 如此一來，hello 備份包含大量的檔案，請參閱大幅縮小程式 hello 時間 toocomplete，完整和增量備份。

- **增強式還原效能**-此版本包含增強功能，可使用大量的檔案時，會大幅提升 hello 還原效能。 如果使用 2-4 百萬個檔案，我們建議您佈建的虛擬陣列 16 GB RAM toosee hello 的增強功能。 當使用少於 2 百萬個檔案，hello hello 虛擬機器的最小需求繼續 toobe 8 GB RAM。

- **改進 tooSupport 封裝**-hello 增強功能，包括登入 hello 磁碟、 CPU、 記憶體、 網路和雲端到 hello 支援封裝，從而提升 hello 的診斷/偵錯裝置問題的程序的統計資料。

- **限制在本機固定的 iSCSI 磁碟區 too200 GB** -本機固定磁碟區，我們建議您在您的 StorSimple Virtual Array 限制 tooa 200 GB iSCSI 磁碟區。 toobe 10%的 hello 佈建磁碟區大小，但的上限為 200 GB，則會繼續 hello 階層式磁碟區的本機保留項目。 

- **備份相關的 bug 修正**-在舊版的軟體，提供了有問題的相關的 toobackups，可能導致備份失敗。 此版本已修正這些錯誤。


## <a name="issues-fixed-in-hello-update-04"></a>Hello 0.4 更新中修正的問題

hello 下表提供此版本中修正問題的摘要。

| 否。 | 功能 | 問題 |
| --- | --- | --- |
| 1 |備份效能|在 hello 較早的版本中 hello 備份包含大量的檔案會花費很長的時間 toocomplete （依 hello 的天數）。 在此版本中，hello 完整和增量備份，請參閱 hello 時間 toocompletion 明顯降低。 |
| 2 |支援封裝|磁碟、 CPU、 記憶體、 網路和雲端統計資料現在會記錄在 toohello 支援檔進行疑難排解任何裝置問題非常有效 hello 支援封裝中。|
| 3 |備份 |在舊版中，長時間執行的備份可能會導致空間無暇 hello 導致備份失敗的裝置上。 在此版本中解決這個問題，藉由使用不超過 5 備份 tooqueue 一次。|
| 4 |iSCSI | 在較早的版本，hello 的階層式或本機固定磁碟區的本機保留會是 hello 佈建磁碟區大小的 10%。 在此版本中，hello 本機保留所有 iSCSI 磁碟區 （本機釘選或階層） 是有限的 too10%期高達最多 200 GB （對於分層磁碟區大於 2 TB） 藉此釋放更多的空間 hello 本機磁碟上。 建議您在此版本中的 hello 固定在本機磁碟區是有限的 too200 GB。|


## <a name="known-issues-in-hello-update-04"></a>Hello 0.4 更新中的已知的問題

hello 下表提供的已知問題摘要 hello StorSimple Virtual Array 並包含 hello hello 舊版本的版本記錄的問題。 

| 否。 | 功能 | 問題 | 因應措施/註解 |
| --- | --- | --- | --- |
| **1.** |更新 |hello hello 預覽版本中建立的虛擬裝置不能更新的 tooa 支援公開上市版本。 |這些虛擬裝置必須容錯 hello 公開上市版本使用災害復原 (DR) 工作流程。 |
| **2.** |佈建的資料磁碟 |一旦您已佈建資料磁碟的某些指定的大小並建立 hello 對應 StorSimple 虛擬裝置，您必須展開或壓縮 hello 資料磁碟。 嘗試在 hello hello 裝置的本機層級中所有的 hello 資料遺失 toodo 結果。 | |
| **3.** |群組原則 |當裝置已加入網域時，套用群組原則可能會影響 hello 裝置作業。 |確定您的虛擬陣列是自己 Active Directory 的組織單位 (OU) 中並沒有群組原則物件 (GPO) 套用的 tooit。 |
| **4.** |本機 Web UI |Internet Explorer (IE ESC) 如有啟用增強式安全性功能，部分本機 Web UI 頁面 (例如 [疑難排解] 或 [維護]) 可能無法正常運作。 這些頁面上的按鈕也可能無法運作。 |關閉 Internet Explorer 中的增強式安全性功能。 |
| **5.** |本機 Web UI |在 HYPER-V 虛擬機器，hello hello web UI 會顯示為 10 Gbps 介面中的網路介面。 |這個行為是 Hyper-V 的反射。 Hyper-V 一律會將虛擬網路介面卡顯示為 10 Gbps。 |
| **6.** |階層式磁碟區或共用 |不支援位元組範圍鎖定處理 hello StorSimple 分層磁碟區的應用程式。 如果啟用位元組範圍鎖定，則 StorSimple 分層無法運作。 |建議的方法包括︰ <br></br>關閉應用程式邏輯中的位元組範圍鎖定。<br></br>選擇此應用程式的 tooput 資料在本機固定磁碟區相對於的 tootiered 磁碟區。<br></br>*需要注意*:，即使之前已完成 hello 還原時使用本機固定磁碟區，且位元組範圍鎖定已啟用，hello 固定在本機磁碟區可以是線上。 在這種情況下，如果還原正在進行中，則您必須等待 hello 還原 toocomplete。 |
| **7.** |階層式共用 |使用大型檔案可能會導致緩慢分層輸出。 |當使用大型檔案，我們建議您該 hello 最大檔案為小於 3 hello 共用大小的百分比。 |
| **8.** |共用的已使用容量 |您可能會看見 hello 共用上的任何資料時，共用耗用量。 這是因為共用的 hello 使用容量包括中繼資料。 | |
| **9.** |災害復原 |您只能執行 hello 災害復原的檔案伺服器 toohello 與 hello 來源裝置相同的網域。 在此版本中不支援災害復原 tooa 另一個網域中的目標裝置。 |新版本將會實作這個功能。 |
| **10.** |Azure PowerShell |無法透過此版本中的 hello Azure PowerShell 管理 hello StorSimple 虛擬裝置。 |您可以透過 hello Azure 傳統入口網站和 hello 本機 web UI 完成所有 hello 管理 hello 虛擬裝置。 |
| **11.** |密碼變更 |hello 虛擬陣列裝置主控台只會接受 EN-US 鍵盤格式中的輸入。 | |
| **12.** |CHAP |CHAP 認證一經建立，即無法移除。 此外，如果您修改 hello CHAP 認證，需要 tootake hello 磁碟區離線，然後使其上線 hello 變更 tootake 效果。 |新版本將會解決此問題。 |
| **13.** |iSCSI 伺服器 |hello '使用的存放裝置' 顯示的 iSCSI 磁碟區可能會不同 hello StorSimple Manager 服務和 hello iSCSI 主機中。 |hello iSCSI 主機有 hello filesystem 檢視。<br></br>hello 裝置會看見 hello hello 的磁碟區是在 hello 大小上限時配置的區塊。 |
| **14.** |檔案伺服器 |如果資料夾的檔案中有替代資料流 （廣告） 與其相關聯，hello 廣告未備份或還原透過災害復原、 複製和項目層級復原。 | |
| **15.** |檔案伺服器 |不支援符號連結。 | |
| **16.** |檔案伺服器 |檔案受保護的 Windows 加密檔案系統 (EFS) 時透過複製或儲存在 hello StorSimple Virtual Array 檔案伺服器會造成不支援的組態中。  | |

## <a name="next-step"></a>後續步驟
在您的 StorSimple Virtual Array 上[安裝 Update 0.4](storsimple-virtual-array-install-update-04.md)。

## <a name="references"></a>參考
要尋找舊版本資訊嗎？ 請移至： 

* [StorSimple Virtual Array Update 0.3 版本資訊](storsimple-ova-update-03-release-notes.md)
* [StorSimple Virtual Array Update 0.1 和 0.2 版本資訊](storsimple-ova-update-01-release-notes.md)
* [StorSimple Virtual Array 正式運作版版本資訊](storsimple-ova-pp-release-notes.md)

