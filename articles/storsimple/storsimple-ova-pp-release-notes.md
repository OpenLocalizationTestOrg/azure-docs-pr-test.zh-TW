---
title: "aaaStorSimple 虛擬陣列版本資訊 |Microsoft 文件"
description: "說明重要的開啟問題和解決方式 hello StorSimple Virtual Array。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 84908160-2b8b-4f4f-a674-f39aaa0bd4de
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/13/2016
ms.author: alkohli
ms.openlocfilehash: ca7b543f95cf5787b7fef39f53887161ebfa7fcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-release-notes"></a>StorSimple Virtual Array 版本資訊
## <a name="overview"></a>概觀
hello 下列版本資訊識別 hello 重大已開啟問題 hello Microsoft Azure StorSimple Virtual Array （也稱為 hello StorSimple 內部部署虛擬裝置或 StorSimple 虛擬 hello hello 2016 年 3 月的公開上市 (GA) 版本裝置）。 這個版本對應 toosoftware 版本 10.0.10271.0。

hello 版本資訊會持續更新，並在發現需要因應措施的重大問題時，會加入。 部署 StorSimple 虛擬裝置之前，請仔細檢閱 hello hello 版本資訊中所包含的資訊。 

hello 下表提供此版本已知問題的摘要。

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

