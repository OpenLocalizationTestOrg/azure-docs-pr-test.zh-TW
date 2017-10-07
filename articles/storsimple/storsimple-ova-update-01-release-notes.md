---
title: "aaaStorSimple 虛擬陣列更新版本資訊 |Microsoft 文件"
description: "描述重要的開啟問題和解決 hello StorSimple Virtual Array 執行 Update 0.2 和 0.1。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3993864d-2ddd-4302-a2f1-8d737fba6eab
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2016
ms.author: alkohli
ms.openlocfilehash: dfd38890feeb667c95134f2adbb35ce2df165620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-02-and-01-release-notes"></a>StorSimple Virtual Array Update 0.2 和 0.1 版本資訊
## <a name="overview"></a>概觀
hello 下列版本資訊找出 hello 重大開啟問題並 hello 更新 Microsoft Azure StorSimple Virtual Array 已解決的問題。 （Microsoft Azure StorSimple Virtual Array 是也稱為 hello StorSimple 內部部署虛擬裝置或 hello StorSimple 虛擬裝置）。 

hello 版本資訊會持續更新，並在發現需要因應措施的重大問題時，會加入。 部署 StorSimple 虛擬裝置之前，請仔細檢閱 hello hello 版本資訊中所包含的資訊。

更新 0.2 對應 toohello 軟體版本**10.0.10280.0**;Update 0.1 是版本**10.0.10279.0**。 hello 的以下各節列出 hello 變更每個更新。 

> [!NOTE]
> 更新是干擾性的，將重新啟動您的裝置。 如果正在進行中的 I/O，hello 裝置會發生停機。
> 
> 

## <a name="issues-fixed-in-hello-update-02"></a>Hello 0.2 更新中修正的問題
更新 0.2 包含從 Update 0.1 的所有變更在加法 toohello 修正 hello 下表中所述：

| 功能 | 問題 |
| --- | --- |
| 更新 |在 hello 最後一個版本中，更新未自動偵測在 hello Azure 傳統入口網站，讓您有 toouse hello 本機 Web UI tooinstall 更新。 此版本已經修正這個問題。 在安裝更新 0.2 之後, 您可以安裝未來的更新使用 hello Azure 傳統入口網站。 |

## <a name="whats-new-in-hello-update-01"></a>在 hello Update 0.1 最新消息
更新 0.1 包含 hello 下列 bug 修正和增強功能。 

* **改善恢復功能的雲端中斷**： 這個版本包含數個 bug 修正周圍災害復原、 備份、 還原及雲端的連線中斷的 hello 事件中的階層處理。 
* **更佳的還原效能**： 此版本中已有大幅縮減 hello hello 還原工作的完成時間的 bug 修正。
* **自動化空間回收最佳化**： 精簡佈建磁碟區上刪除資料時，hello 未使用的儲存體必須區塊 toobe 回收。 此版本有改善的 hello 空間回收處理序從 hello 雲端導致 hello 未使用空間變成可用速度為比較的 toohello 先前版本。
* **新的虛擬磁碟映像**： 新的 VHD、 VHDX 和 VMDK，現在都透過 hello Azure 傳統入口網站。 您可以下載這些映像 tooprovision 新更新 0.1 裝置。
* **改善的 hello 入口網站中的作業狀態的 hello 精確度**: hello 在舊版的軟體，hello 入口網站中的報告工作狀態是不精細。 本版已經修正這個問題。
* **網域聯結經驗**: Bug 修正相關 toodomain 聯結和 hello 裝置的重新命名。

## <a name="issues-fixed-in-hello-update-01"></a>Hello 0.1 更新中修正的問題
hello 下表提供此版本中修正問題的摘要。

| 否。 | 功能 | 問題 |
| --- | --- | --- |
| 1 |VMDK |在某些 VMware 版本，hello OS 磁碟已被視為疏鬆導致警示與干擾一般作業。 本版已修正這個問題。 |
| 2 |iSCSI 伺服器 |在 hello 最後一個版本中，需要的 toospecify StorSimple 虛擬裝置的每個啟用的網路介面的閘道已 hello 使用者。 在此版本中變更此行為，讓 hello 使用者擁有 tooconfigure 所有 hello 啟用網路介面的至少一個閘道。 |
| 3 |支援封裝 |在 hello 舊版軟體中支援 hello 封包大小大於 1 GB 時失敗的封裝集合。 此版本已經修正這個問題。 |
| 4 |雲端存取 |在 hello 最後一個版本中，如果 hello StorSimple Virtual Array 沒有網路連線，且已重新啟動，hello 本機 UI 會有連線問題。 本版已修正這個問題。 |
| 5 |監視圖表 |在 hello 先前版本中，裝置容錯移轉之後 hello 雲端容量使用率圖表會顯示 hello Azure 傳統入口網站中的值不正確。 這被固定的 hello 目前版本中。 |

## <a name="known-issues-in-hello-update-01"></a>在 hello Update 0.1 的已知的問題
hello 下表提供的已知問題摘要 hello StorSimple Virtual Array 並包含 hello hello 舊版本的版本記錄的問題。 **hello 這個版本中所述的問題版本會以星號標示。這份清單中的幾乎所有 hello 問題有都轉從 StorSimple Virtual Array hello GA 版本。**

| 否。 | 功能 | 問題 | 因應措施/註解 |
| --- | --- | --- | --- |
| **1.** |更新 |hello hello 預覽版本中建立的虛擬裝置不能更新的 tooa 支援公開上市版本。 |這些虛擬裝置必須容錯 hello 公開上市版本使用災害復原 (DR) 工作流程。 |
| **2.** |佈建的資料磁碟 |一旦您已佈建資料磁碟的某些指定的大小並建立 hello 對應 StorSimple 虛擬裝置，您必須展開或壓縮 hello 資料磁碟。 嘗試 toodo 因此將會導致在 hello hello 裝置的本機層級中所有的 hello 資料遺失。 | |
| **3.** |群組原則 |當裝置已加入網域時，套用群組原則可能會影響 hello 裝置作業。 |確定您的虛擬陣列是自己 Active Directory 的組織單位 (OU) 中並沒有群組原則物件 (GPO) 套用的 tooit。 |
| **4.** |本機 Web UI |Internet Explorer (IE ESC) 如有啟用增強式安全性功能，部分本機 Web UI 頁面 (例如 [疑難排解] 或 [維護]) 可能無法正常運作。 這些頁面上的按鈕也可能無法運作。 |關閉 Internet Explorer 中的增強式安全性功能。 |
| **5.** |本機 Web UI |在 HYPER-V 虛擬機器，hello hello web UI 會顯示為 10 Gbps 介面中的網路介面。 |這個行為是 Hyper-V 的反射。 Hyper-V 一律會將虛擬網路介面卡顯示為 10 Gbps。 |
| **6.** |階層式磁碟區或共用 |不支援位元組範圍鎖定處理 hello StorSimple 分層磁碟區的應用程式。 如果啟用位元組範圍鎖定，則 StorSimple 分層無法運作。 |建議的方法包括︰ <br></br>關閉應用程式邏輯中的位元組範圍鎖定。<br></br>選擇此應用程式的 tooput 資料在本機固定磁碟區相對於的 tootiered 磁碟區。<br></br>*需要注意*： 如果使用本機固定磁碟區，且位元組範圍鎖定已啟用，請注意即使之前已完成 hello 還原 hello 固定在本機磁碟區可以是線上。 在這種情況下，如果還原正在進行中，則您必須等待 hello 還原 toocomplete。 |
| **7.** |階層式共用 |使用大型檔案可能會導致緩慢分層輸出。 |當使用大型檔案，我們建議您該 hello 最大檔案為小於 3 hello 共用大小的百分比。 |
| **8.** |共用的已使用容量 |您可能會看見 hello 沒有 hello 共用上的任何資料的共用耗用量。 這是因為共用的 hello 使用容量包括中繼資料。 | |
| **9.** |災害復原 |您只能執行 hello 災害復原的檔案伺服器 toohello 與 hello 來源裝置相同的網域。 在此版本中不支援災害復原 tooa 另一個網域中的目標裝置。 |新版本將會實作這個功能。 |
| **10.** |Azure PowerShell |無法透過此版本中的 hello Azure PowerShell 管理 hello StorSimple 虛擬裝置。 |您可以透過 hello Azure 傳統入口網站和 hello 本機 web UI 完成所有 hello 管理 hello 虛擬裝置。 |
| **11.** |密碼變更 |hello 虛擬陣列裝置主控台只會接受 EN-US 鍵盤格式中的輸入。 | |
| **12.** |CHAP |CHAP 認證一經建立，即無法移除。 此外，如果您修改 hello CHAP 認證時，您將需要 tootake hello 磁碟區離線，並再使其上線 hello 變更 tootake 效果。 |這些問題在新版本中都會獲得解決。 |
| **13.** |iSCSI 伺服器 |hello '使用的存放裝置' 顯示的 iSCSI 磁碟區可能會不同 hello StorSimple Manager 服務和 hello iSCSI 主機中。 |hello iSCSI 主機有 hello filesystem 檢視。<br></br>hello 裝置會看見 hello hello 的磁碟區是在 hello 大小上限時配置的區塊。 |
| **14.** |檔案伺服器* |如果資料夾的檔案中有替代資料流 （廣告） 與其相關聯，hello 廣告未備份或還原透過災害復原、 複製和項目層級復原。 | |

## <a name="next-step"></a>後續步驟
[安裝更新](storsimple-ova-install-update-01.md) 。

