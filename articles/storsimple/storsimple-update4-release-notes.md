---
title: "aaaStorSimple 8000 系列 Update 4 版本資訊 |Microsoft 文件"
description: "適用於 StorSimple 8000 系列 Update 4 描述 hello 新功能、 問題和因應措施。"
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
ms.date: 04/04/2017
ms.author: alkohli
ms.openlocfilehash: 4bca8ca222e6706fd6eaf56b702b0d34b6ffd1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-4-release-notes"></a>StorSimple 8000 系列 Update 4 版本資訊

## <a name="overview"></a>概觀

hello 下列版本資訊說明 hello 新功能並識別適用於 StorSimple 8000 系列 Update 4 hello 重要的議題。 也會包含在此版本中所包含的 hello StorSimple 軟體更新清單。 

更新 4 可以透過更新 3.1 執行版本 (GA) 或 Update 0.1 套用的 tooany StorSimple 裝置。 更新 4 與相關聯的 hello 裝置版本是 6.3.9600.17820。

請檢閱附註，然後再部署 hello 更新您的 StorSimple 解決方案中的 hello 版本中所包含的 hello 資訊。

> [!IMPORTANT]
> * Update 4 包含裝置軟體、USM 韌體、LSI 驅動程式與韌體、磁碟韌體、Storport 和 Spaceport、 安全性及其他 OS 更新。 它會採用大約 4 小時 tooinstall 這項更新。 磁碟韌體更新是干擾性更新，會導致您的裝置停機。 我們建議您套用 Update 4 tookeep 您最新的裝置。 
> * 新的版本，您可能不會看到更新立即，因為我們會執行 hello 更新分階段導入。 請等候數天然後再次掃描更新，因為很快就會提供更新。

## <a name="whats-new-in-update-4"></a>Update 4 的新功能

hello 下列索引鍵的改進和 bug 修正已進行更新 4 中。

* **更聰明的自動化空間回收演算法**– 在更新 4 中，hello 自動化的空間回收的演算法為增強的 tooadjust hello 空間回收循環根據預期的 hello 回收 hello 雲端中的可用空間。 

* **本機固定磁碟區的效能增強功能**– 更新 4 已改善 hello 效能有很高的資料擷取 （資料比較 toovolume 大小） 的案例中的本機固定磁碟區。

* **Heatmap 還原**-在 hello 稍早的版本中，下列的災害復原 (DR) 期間，hello 資料已從 hello 雲端式導致效能變慢的 hello 存取模式上還原。 

    新功能實作更新 4 中使用先前 tooDR hello 裝置時，追蹤經常存取資料 toocreate heatmap (最常使用的資料區塊有高駐點熱度圖，而小於用區塊有熱度)。 DR 之後, StorSimple 使用 hello heatmap tooautomatically 還原和解除凍結 hello hello 雲端的資料。 

    所有的 hello 還原現在都是根據 heatmap 還原。 如需有關如何 tooquery] 和 [取消 heatmap 基礎還原和解除凍結工作的詳細資訊，請移過[Windows PowerShell for StorSimple cmdlet 參考](https://technet.microsoft.com/library/dn688168.aspx)。

* **StorSimple 診斷工具**– 在更新 4 中，StorSimple 診斷工具正在釋放 tooallow 容易診斷，以及問題的疑難排解相關 toosystem、 網路、 效能和硬體元件健全狀況。 透過 hello Windows PowerShell for StorSimple 執行這個工具。 如需詳細資訊，請移至太[使用 StorSimple 診斷工具疑難排解](storsimple-8000-diagnostics.md)。

* **UI 為基礎的 StorSimple 移轉工具**-先前 toothis 發行，請從 5000 7000 系列移轉資料所需的 hello 使用者 tooexecute hello 移轉工作流程使用 hello Azure PowerShell 介面的一部分。 在此版本中，簡單易用之 UI 為基礎的 StorSimple 移轉工具將可支援 toofacilitate hello 相同移轉工作流程。 此工具也會讓復原的貯體的 hello 彙總。 

* **FIPS 相關變更**-這個發行版本及更新版本，同時 hello Microsoft Azure 政府和 Azure 公用雲端帳戶的預設上所有的 hello StorSimple 8000 系列裝置便會啟用 FIPS。

* **更新變更**-在此版本中，已經修正失敗的錯誤相關 tooupdate。

* **磁碟失敗警示**-在此版本中加入新的警示，警告使用者即將發生磁碟失敗 hello。 如果您遇到此警示，請連絡 Microsoft 支援服務 tooship 取代磁碟。 如需詳細資訊，請移至太[StorSimple 裝置上的硬體警示](storsimple-manage-alerts.md#hardware-alerts)。

* **控制器更換變更**-在此版本中加入 cmdlet，可讓 hello 使用者 tooquery hello hello 控制器更換程序狀態。 如需詳細資訊，請移至 toohello [cmdlet tooquery 控制器更換狀態](https://technet.microsoft.com/library/dn688168.aspx)。


## <a name="issues-fixed-in-update-4"></a>Update 4 中修正的問題

hello 下表提供更新 4 中已修正的問題的摘要。    

| 否 | 功能 | 問題 | 適用於 toophysical 裝置 | 適用於 toovirtual 裝置 |
| --- | --- | --- | --- | --- |
| 1 |容錯移轉 |在 hello 較早版本中的，hello 容錯移轉之後，那里已相關的問題 toocleanup 觀察到 hello 客戶站台。 此版本已經修正這個問題。 |是 |是 |
| 2 |固定在本機的磁碟區 |Hello 舊版時發生問題 toorelated 建立磁碟區的磁碟區建立失敗會導致本機固定磁碟區。 此版本已找出此問題的根本原因並加以修正。 |是 |否 |
| 3 |支援封裝 |在先前版本中，沒有問題相關的 tooSupport 套件會導致 System.OutOfMemory 例外狀況或其他支援封裝建立失敗所導致的錯誤。 此版本已經修正這些錯誤。 |是 |是 |
| 4 |監視 |在先前版本中，那里相關的問題 toomonitoring 圖表固定在本機磁碟區所在耗用量是以 EB。 此版本已經解決這個錯誤。 |是 |是 |
| 5 |移轉 |在先前版本中，沒有從 5000 7000 系列 too8000 系列裝置移轉的幾個問題相關的 toohello 可靠性。 此版本已經解決這些問題。 |是 |是 |
| 6 |更新 |在舊版中，如果發生更新失敗、 hello 控制站會進入修復模式，而且因此 hello 使用者無法繼續 hello 更新需要 toocontact Microsoft 支援服務。 <br> 這個行為在此版本中已變更。 如果兩個 hello 控制器之後 hello 使用者更新失敗執行 hello 相同版本 (更新 4)，控制站不會進入修復模式的 hello。 如果 hello 使用者遇到此失敗，則建議您在等候的位元，，然後重試 hello 更新。 hello 重試將會成功。 如果 hello 重試失敗，它們應該連絡 Microsoft 支援。 |是 |是 |


## <a name="known-issues-in-update-4-from-previous-releases"></a>Update 4 中舊版的已知問題

Update 4 中沒有新的已知問題。 如轉 tooUpdate 4 舊版問題的清單，請移至太[Update 3 版本資訊](storsimple-update3-release-notes.md#known-issues-in-update-3)。

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-update-4"></a>Update 4 中的序列連結 SCSI (SAS) 控制器和韌體更新

此版本包含 SAS 控制器和 LSI 驅動程式與韌體的更新。 如需有關如何 tooinstall 這些更新，請參閱[安裝 Update 4](storsimple-install-update-4.md) StorSimple 裝置上。

## <a name="virtual-device-updates-in-update-4"></a>Update 4 中的虛擬裝置更新

此更新不能套用的 toohello StorSimple 雲端應用裝置 （也稱為 hello 虛擬裝置）。 將新的虛擬裝置必須 toobe 建立。 

## <a name="next-step"></a>後續步驟

了解如何太[安裝 Update 4](storsimple-install-update-4.md) StorSimple 裝置上。

