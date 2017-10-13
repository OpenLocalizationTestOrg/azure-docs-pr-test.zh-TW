---
title: "StorSimple Virtual Array Update 0.6 版本資訊 | Microsoft Docs"
description: "描述執行 Update 0.6 之 StorSimple Virtual Array 的重大未決問題和解決方式。"
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
ms.openlocfilehash: af202cf652300ee7897eb2dede33f38058fc2837
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="storsimple-virtual-array-update-06-release-notes"></a>StorSimple Virtual Array Update 0.6 版本資訊

## <a name="overview"></a>概觀

下列版本資訊指出 Microsoft Azure StorSimple Virtual Array 更新的重大未決問題和已解決問題。

版本資訊會持續更新，並在發現需要提出因應措施的重大問題時有所增補。 部署 StorSimple Virtual Array 之前，請仔細檢閱版本資訊中所含的資訊。

Update 0.6 與軟體版本 **10.0.10293.0** 對應。

> [!IMPORTANT]
> - 更新是干擾性作業，會重新啟動您的裝置。 如果 I/O 正在進行中，裝置就會停機。 如需有關如何套用更新的詳細指示，請移至[安裝 Update 0.6](storsimple-virtual-array-install-update-06.md)。
>
> - 我們強烈建議您安裝 Update 0.6，因為它包含重要的安全性問題修正。


## <a name="whats-new-in-the-update-06"></a>Update 0.6 的新功能
Update 0.6 是重大更新，應該立即部署。 此更新包含下列修正： 

- **Windows 安全性問題修正** - 此版本有 **Windows 重大安全性問題修正**。 檢閱下列安全性更新，以取得有關安全性問題和相關修正的詳細資訊：
    - [2016 年 12 月適用於 Windows 8.1 和 Windows Server 2012 R2 的僅限安全性品質更新](https://support.microsoft.com/help/3205400/december-2016-security-only-quality-update-for-windows-8.1-and-windows-server-2012-r2)
    - [March 2017 年 3 月適用於 Windows 8.1 和 Windows Server 2012 R2 的僅限安全性品質更新](https://support.microsoft.com/help/4012213/march-2017-security-only-quality-update-for-windows-8-1-and-windows-server-2012-r23)
    - [2017 年 5 月 9 日—KB4019213 (僅限安全性更新)](https://support.microsoft.com/help/4019213/windows-8-update-kb4019213)

- **還原修正** - 舊版中有個錯誤，讓還原作業無法完成。 此版本已經修正這個錯誤。


## <a name="issues-fixed-in-the-update-06"></a>Update 0.6 中修正的問題

下表提供本版已修正問題的摘要。

| 編號 | 功能 | 問題 |
| --- | --- | --- |
| 1 |安全性| 此版本包含重大的 Windows 安全性更新。 我們建議您立即安裝此更新。|
| 2 |還原| 在還原期間發生競爭情形，讓還原作業無法完成。 BUG 修正會解決此競爭情形。|


## <a name="known-issues-in-the-update-06"></a>Update 0.6 的已知問題

下表提供 StorSimple Virtual Array 的已知問題摘要，並包含舊版所列的問題。

| 否。 | 功能 | 問題 | 因應措施/註解 |
| --- | --- | --- | --- |
| **1.** |更新 |預覽版中所建立的虛擬裝置無法更新為支援的正式運作版本。 |必須針對正式運作版本使用災害復原 (DR) 工作流程容錯移轉這些虛擬裝置。 |
| **2.** |佈建的資料磁碟 |佈建特定指定大小的資料磁碟並建立對應的 StorSimple 虛擬裝置之後，不得展開或壓縮資料磁碟。 嘗試執行會導致裝置本機層中的所有資料遺失。 | |
| **3.** |群組原則 |若裝置已加入網域，套用群組原則可能會對裝置運作產生不良的影響。 |確定您的虛擬陣列位於它自己的 Active Directory 組織單位 (OU) 中，且沒有套用群組原則物件 (GPO)。 |
| **4.** |本機 Web UI |Internet Explorer (IE ESC) 如有啟用增強式安全性功能，部分本機 Web UI 頁面 (例如 [疑難排解] 或 [維護]) 可能無法正常運作。 這些頁面上的按鈕也可能無法運作。 |關閉 Internet Explorer 中的增強式安全性功能。 |
| **5.** |本機 Web UI |在 Hyper-V 虛擬機器中，Web UI 中的網路介面會顯示為 10 Gbps 介面。 |這個行為是 Hyper-V 的反射。 Hyper-V 一律會將虛擬網路介面卡顯示為 10 Gbps。 |
| **6.** |階層式磁碟區或共用 |不支援使用 StorSimple 階層式磁碟區之應用程式的位元組範圍鎖定。 如果啟用位元組範圍鎖定，則 StorSimple 分層無法運作。 |建議的方法包括︰ <br></br>關閉應用程式邏輯中的位元組範圍鎖定。<br></br>選擇將這個應用程式的資料放在固定在本機的磁碟區中，而非階層式磁碟區。<br></br>警告：使用固定在本機的磁碟區，並啟用位元組範圍鎖定時，固定在本機的磁碟區可以上線，即使在還原完成之前也是一樣。 在這種情況下，如果正在還原，則必須等待還原完成。 |
| **7.** |階層式共用 |使用大型檔案可能會導致緩慢分層輸出。 |使用大型檔案時，建議最大檔案不要超過共用大小的 3%。 |
| **8.** |共用的已使用容量 |您可能會在共用上沒有任何資料時看到共用耗用量。 這是因為共用的已使用容量包括中繼資料。 | |
| **9.** |災害復原 |您只能對與來源裝置網域相同的網域執行檔案伺服器的災害復原。 這個版本不支援另一個網域中目標裝置的災害復原。 |新版本將會實作這個功能。 如需詳細資訊，請移至 [StorSimple Virtual Array 的容錯移轉和災害復原](storsimple-virtual-array-failover-dr.md) |
| **10.** |Azure PowerShell |在這版本中，無法透過 Azure PowerShell 管理 StorSimple 虛擬裝置。 |所有虛擬裝置管理都應該透過 Azure 入口網站和本機 Web UI 來完成。 |
| **11.** |密碼變更 |虛擬陣列裝置主控台僅接受美式鍵盤格式的輸入。 | |
| **12.** |CHAP |CHAP 認證一經建立，即無法移除。 此外，如果您修改 CHAP 認證，就必須先讓磁碟區離線再上線，變更才會生效。 |新版本將會解決此問題。 |
| **13.** |iSCSI 伺服器 |針對 iSCSI 磁碟區顯示的 [已使用的儲存體] 在 StorSimple Device Manager 服務與 iSCSI 主機中可能不同。 |ISCSI 主機具有檔案系統檢視。<br></br>裝置會在達到磁碟區大小上限時，看到所配置的區塊。 |
| **14.** |檔案伺服器 |如果資料夾中的檔案中有與其相關聯的替代資料流 (ADS)，就不會透過災害復原、複製和項目層級復原來備份或還原 ADS。 | |
| **15.** |檔案伺服器 |不支援符號連結。 | |
| **16.** |檔案伺服器 |如果將 Windows 加密檔案系統 (EFS) 保護的檔案複製或儲存到 StorSimple 虛擬陣列檔案伺服器，將會導致不支援的組態。  | |
| **17.** |更新 |如果透過本機 UI 嘗試安裝 Hotfix 時看到錯誤代碼：2359302 (十六進位 0x240006)，表示您的裝置上已安裝了 Hotfix。   | |

## <a name="next-step"></a>後續步驟
在 StorSimple Virtual Array 上[安裝 Update 0.6](storsimple-virtual-array-install-update-06.md)。

## <a name="references"></a>參考
要尋找舊版本資訊嗎？ 請移至：

* [StorSimple Virtual Array Update 0.5 版本資訊](storsimple-virtual-array-update-05-release-notes.md)
* [StorSimple Virtual Array Update 0.4 版本資訊](storsimple-virtual-array-update-04-release-notes.md)
* [StorSimple Virtual Array Update 0.3 版本資訊](storsimple-ova-update-03-release-notes.md)
* [StorSimple Virtual Array Update 0.1 和 0.2 版本資訊](storsimple-ova-update-01-release-notes.md)
* [StorSimple Virtual Array 正式運作版版本資訊](storsimple-ova-pp-release-notes.md)

