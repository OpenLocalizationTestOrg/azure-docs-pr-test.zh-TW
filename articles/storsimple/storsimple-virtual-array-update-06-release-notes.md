---
title: "aaaStorSimple 虛擬陣列更新 0.6 的版本資訊 |Microsoft 文件"
description: "描述重要開啟問題和解決 hello StorSimple Virtual Array 執行更新 0.6。"
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
ms.date: 05/24/2017
ms.author: alkohli
ms.openlocfilehash: 7b573457dc07ce41e95d49d66ccc174045f31a42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-06-release-notes"></a>StorSimple Virtual Array Update 0.6 版本資訊

## <a name="overview"></a>概觀

hello 下列版本資訊找出 hello 重大開啟問題並 hello 更新 Microsoft Azure StorSimple Virtual Array 已解決的問題。

hello 版本資訊會持續更新，並在發現需要因應措施的重大問題時，會加入。 部署 StorSimple 虛擬陣列之前，請仔細檢閱 hello hello 版本資訊中所包含的資訊。

更新 0.6 對應 toohello 軟體版本**10.0.10293.0**。

> [!IMPORTANT]
> - 更新是干擾性作業，會重新啟動您的裝置。 如果正在進行中的 I/O，hello 裝置會產生停機時間。 如需如何 tooapply hello 更新的詳細指示，請移過[安裝更新 0.6](storsimple-virtual-array-install-update-06.md)。
>
> - 我們強烈建議您安裝 Update 0.6，因為它包含重要的安全性問題修正。


## <a name="whats-new-in-hello-update-06"></a>新功能更新 0.6 hello
Update 0.6 是重大更新，應該立即部署。 此更新包含下列修正 hello: 

- **Windows 安全性問題修正** - 此版本有 **Windows 重大安全性問題修正**。 檢閱下列有關 hello 安全性問題的詳細資訊的安全性更新的 hello 和 hello 相關聯的修正程式：
    - [2016 年 12 月適用於 Windows 8.1 和 Windows Server 2012 R2 的僅限安全性品質更新](https://support.microsoft.com/help/3205400/december-2016-security-only-quality-update-for-windows-8.1-and-windows-server-2012-r2)
    - [March 2017 年 3 月適用於 Windows 8.1 和 Windows Server 2012 R2 的僅限安全性品質更新](https://support.microsoft.com/help/4012213/march-2017-security-only-quality-update-for-windows-8-1-and-windows-server-2012-r23)
    - [2017 年 5 月 9 日—KB4019213 (僅限安全性更新)](https://support.microsoft.com/help/4019213/windows-8-update-kb4019213)

- **還原修正**-中較早的版本時發生錯誤，因而阻止 hello 還原無法完成。 此版本已經修正這個錯誤。


## <a name="issues-fixed-in-hello-update-06"></a>Hello 0.6 更新中修正的問題

hello 下表提供此版本中修正問題的摘要。

| 否。 | 功能 | 問題 |
| --- | --- | --- |
| 1 |安全性| 此版本包含重大的 Windows 安全性更新。 我們建議您立即安裝此更新。|
| 2 |還原| 在還原期間，發生的競爭情況會使 hello 還原作業無法完成。 hello bug 修正可解決這種競爭情形。|


## <a name="known-issues-in-hello-update-06"></a>Hello 更新 0.6 的已知的問題

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
| **8.** |共用的已使用容量 |您可能會看見 hello 共用上的任何資料時，共用耗用量。 此耗用量是因為使用 hello 容量共用包含中繼資料。 | |
| **9.** |災害復原 |您只能執行 hello 災害復原的檔案伺服器 toohello 與 hello 來源裝置相同的網域。 在此版本中不支援災害復原 tooa 另一個網域中的目標裝置。 |新版本將會實作這個功能。 如需詳細資訊，請移至太[容錯移轉和災害復原您的 StorSimple Virtual Array](storsimple-virtual-array-failover-dr.md) |
| **10.** |Azure PowerShell |無法透過此版本中的 hello Azure PowerShell 管理 hello StorSimple 虛擬裝置。 |所有 hello 管理 hello 虛擬裝置應該都透過 hello Azure 入口網站與 hello 本機 web UI。 |
| **11.** |密碼變更 |hello 虛擬陣列裝置主控台只接受輸入中 en-我們鍵盤格式。 | |
| **12.** |CHAP |CHAP 認證一經建立，即無法移除。 此外，如果您修改 hello CHAP 認證，需要 tootake hello 磁碟區離線，然後使其上線 hello 變更 tootake 效果。 |新版本將會解決此問題。 |
| **13.** |iSCSI 伺服器 |hello '使用的存放裝置' 顯示的 iSCSI 磁碟區可能會不同 hello StorSimple 裝置管理員服務和 hello iSCSI 主機中。 |hello iSCSI 主機有 hello filesystem 檢視。<br></br>hello 裝置會看見 hello hello 的磁碟區是在 hello 大小上限時配置的區塊。 |
| **14.** |檔案伺服器 |如果資料夾的檔案中有替代資料流 （廣告） 與其相關聯，hello 廣告未備份或還原透過災害復原、 複製和項目層級復原。 | |
| **15.** |檔案伺服器 |不支援符號連結。 | |
| **16.** |檔案伺服器 |檔案受保護的 Windows 加密檔案系統 (EFS) 時透過複製或儲存在 hello StorSimple Virtual Array 檔案伺服器會造成不支援的組態中。  | |
| **17.** |更新 |如果您看到錯誤程式碼： 2359302 （十六進位 0x240006） 時，嘗試透過 hotfix tooinstall hello 本機 UI，則這表示您的裝置上已安裝該 hello hotfix。   | |

## <a name="next-step"></a>後續步驟
在 StorSimple Virtual Array 上[安裝 Update 0.6](storsimple-virtual-array-install-update-06.md)。

## <a name="references"></a>參考
要尋找舊版本資訊嗎？ 請移至：

* [StorSimple Virtual Array Update 0.5 版本資訊](storsimple-virtual-array-update-05-release-notes.md)
* [StorSimple Virtual Array Update 0.4 版本資訊](storsimple-virtual-array-update-04-release-notes.md)
* [StorSimple Virtual Array Update 0.3 版本資訊](storsimple-ova-update-03-release-notes.md)
* [StorSimple Virtual Array Update 0.1 和 0.2 版本資訊](storsimple-ova-update-01-release-notes.md)
* [StorSimple Virtual Array 正式運作版版本資訊](storsimple-ova-pp-release-notes.md)

