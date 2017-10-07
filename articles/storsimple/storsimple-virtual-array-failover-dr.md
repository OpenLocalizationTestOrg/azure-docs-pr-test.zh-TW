---
title: "aaaStorSimple 虛擬陣列災害復原和裝置容錯移轉 |Microsoft 文件"
description: "深入了解如何 toofailover StorSimple 虛擬陣列。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 3c1f9c62-af57-4634-a0d8-435522d969aa
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5f125efd1ffb94489cdfa7cfaafae7d57cc10131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-and-device-failover-for-your-storsimple-virtual-array-via-azure-portal"></a>透過 Azure 入口網站進行 StorSimple Virtual Array 的災害復原和裝置容錯移轉

## <a name="overview"></a>概觀
本文說明 hello 嚴重損壞修復您的 Microsoft Azure StorSimple 虛擬陣列包括 hello 詳細步驟 toofail 透過 tooanother 虛擬陣列。 在容錯移轉可讓您 toomove 資料從*來源*裝置 hello datacenter tooa*目標*裝置。 hello 目標裝置可能在相同或不同的地理位置位於 hello。 hello 裝置容錯移轉是 hello 整個裝置。 容錯移轉期間，hello hello 來源裝置的雲端資料會變更擁有權 toothat 的 hello 目標裝置。

本文是只適用 tooStorSimple 虛擬陣列。 8000 系列裝置，透過 toofail 移過[您的 StorSimple 裝置的裝置容錯移轉和災害復原](storsimple-device-failover-disaster-recovery.md)。

## <a name="what-is-disaster-recovery-and-device-failover"></a>什麼是災害復原和裝置容錯移轉？

在災害復原 (DR) 案例中，hello 主要裝置會停止運作。 在此案例中，您可以移動 hello 與 hello 失敗的裝置 tooanother 裝置相關聯的雲端資料。 您可以使用 hello 主要裝置當做 hello*來源*並指定另一個裝置當做 hello*目標*。 此程序為參照的 tooas hello*容錯移轉*。 容錯移轉期間，所有 hello 磁碟區，或從 hello 來源裝置 hello 共用變更擁有權，而且傳送的 toohello 目標裝置。 允許 hello 資料沒有篩選。

DR 會模型化為使用 hello 熱度圖型階層處理及追蹤完整的裝置還原。 熱門地圖是由指派熱度值 toohello 根據資料的讀取和寫入模式中定義。 此熱度對應則層 hello 最低熱資料區塊 （chunk） toohello 雲端第一次同時 hello 本機層中的 hello 高 （最常使用） 的熱資料區塊。 在 DR 期間，StorSimple 使用 hello 熱度圖 toorestore 和解除凍結 hello hello 雲端的資料。 hello 裝置擷取所有 hello 磁碟區/共用 hello 最後一個新的備份中 （如同取決於在內部），並會從該備份執行還原。 hello 虛擬陣列會協調 hello 整個 DR 程序。

> [!IMPORTANT]
> 在裝置容錯移轉的 hello 結尾刪除 hello 來源裝置，因此不支援容錯回復。
> 
> 

嚴重損壞修復協調透過 hello 裝置容錯移轉功能，並起始從 hello**裝置**刀鋒視窗。 此刀鋒視窗會製為表格所有 hello StorSimple 裝置連線的 tooyour StorSimple 裝置管理員服務。 對於每個裝置，您可以查看 hello 易記名稱、 狀態、 已佈建和最大容量、 類型和模型。

## <a name="prerequisites-for-device-failover"></a>裝置容錯移轉需求

### <a name="prerequisites"></a>必要條件

裝置容錯移轉，請確定符合下列必要條件，hello:

* hello 來源裝置必須在 toobe **Deactivated**狀態。
* hello 目標裝置需要 tooshow 向上為**已 tooset 準備註冊**hello Azure 入口網站中。 佈建 hello 的目標虛擬陣列相同或更高的容量。 使用 hello 本機 web UI tooconfigure，成功註冊 hello 目標虛擬陣列。
  
  > [!IMPORTANT]
  > 請勿嘗試 tooconfigure hello 註冊虛擬裝置透過 hello 服務。 任何裝置設定應該透過 hello 服務來不執行。
  > 
  > 
* hello 目標裝置不能有名稱為 hello 來源裝置相同的 hello。
* hello 來源和目標裝置沒有 toobe hello 相同的型別。 您只可以容錯移轉設定為檔案伺服器 tooanother 檔案伺服器的虛擬陣列。 hello 也適用於 iSCSI 伺服器。
* 針對檔案伺服器 DR，我們建議您加入 hello 目標裝置 toohello hello 來源相同的網域。 此組態可確保 hello 共用權限會自動進行解析。 只有 hello 容錯移轉 tooa 目標裝置 hello 中的相同的網域。
* hello dr 的可用目標裝置所擁有的裝置 hello 相同或較大的容量相較 toohello 來源裝置。 hello 裝置所連接的 tooyour 服務但不是符合 hello 做為目標裝置沒有足夠空間標準。

### <a name="other-considerations"></a>其他考量

* 規劃的容錯移轉 
  
  * 我們建議您先進行離線 hello 來源裝置上所有 hello 磁碟區或共用。
  * 我們建議您進行 hello 裝置的備份，並再繼續 hello 容錯移轉 toominimize 遺失資料。 
* 未規劃的容錯移轉，hello 裝置會使用 hello 最新備份 toorestore hello 資料。

### <a name="device-failover-prechecks"></a>裝置容錯移轉前置檢查

Hello DR 開始之前, hello 裝置執行 prechecks。 這些檢查有助於確保 DR 開始時不會發生任何錯誤。 hello prechecks 包括：

* 正在驗證 hello 儲存體帳戶。
* 正在檢查 hello 雲端連線 tooAzure。
* 正在檢查 hello 目標裝置上的可用空間。
* 檢查 iSCSI 伺服器來源裝置磁碟區是否有
  
  * 有效的 ACR 名稱。
  * 有效的 IQN (不超過 220 個字元)。
  * 有效的 CHAP 密碼 (長度為 12-16 個字元)。

如果任何上述 prechecks hello 失敗，您無法進行 hello DR。 解決這些問題，然後重試 DR。

Hello DR 順利完成之後，hello hello 雲端上的資料 hello 來源裝置的擁有權會是傳送的 toohello 目標裝置。 hello 來源裝置就不再 hello 入口網站中，您可以使用。 存取 tooall hello 磁碟區/共用 hello 來源裝置上遭到封鎖，hello 目標裝置會變成作用中。

> [!IMPORTANT]
> Hello 裝置已無法再使用，雖然 hello 您 hello 主機系統佈建的虛擬機器仍然會消耗資源。 Hello DR 順利完成之後，您可以從主機系統來刪除此虛擬機器。
> 
> 

## <a name="fail-over-tooa-virtual-array"></a>容錯移轉 tooa 虛擬陣列

執行此程序之前，建議您先佈建、設定另一個 StorSimple Virtual Array 並向 StorSimple 裝置管理員服務註冊。

> [!IMPORTANT]
> 
> * 您無法從 StorSimple 8000 系列裝置 tooa 1200 虛擬裝置容錯移轉。
> * 您可以從美國聯邦資訊處理標準 (FIPS) 啟用虛擬裝置 tooanother FIPS 已啟用的裝置或 tooa 非 FIPS 裝置 hello 政府入口網站中部署容錯移轉。


執行下列步驟 toorestore hello tooa 目標 StorSimple 虛擬裝置 hello。

1. 佈建及設定的目標裝置符合 hello[用於裝置容錯移轉的必要條件](#prerequisites)。 完成透過 hello 本機 web UI 的 hello 裝置設定，然後登錄 tooyour StorSimple 裝置管理員服務。 如果建立檔案伺服器，請移至的 toostep 1[設定為檔案伺服器](storsimple-virtual-array-deploy3-fs-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device)。 如果建立 iSCSI 伺服器，請移至的 toostep 1[設定 iSCSI 伺服器為](storsimple-virtual-array-deploy3-iscsi-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device)。

2. Hello 主機上讓磁碟區/共用離線。 tootake hello 磁碟區/共用離線，請參閱 「 hello 主機 toohello 作業系統特定指示。 如果沒有已經離線，您需要 tootake 所有 hello 磁碟區/共用離線 hello 裝置上執行 hello 下列。
   
    1. 跳過**裝置**刀鋒視窗中，選取您的裝置。
   
    2. 跳過**設定 > 管理 > 共用**(或**設定 > 管理 > 磁碟區**)。 
   
    3. 選取共用/磁碟區，按一下滑鼠右鍵並選取 [離線]。 
   
    4. 當提示確認時，會檢查**我了解 hello 影響離線此共用。** 
   
    5. 按一下 [離線]。

3. 在您的 StorSimple 裝置管理員服務移過**管理 > 裝置**。 在 hello**裝置**刀鋒視窗中，選取，然後按一下 來源裝置。

4. 在 [裝置儀表板] 刀鋒視窗中，按一下 [停用]。

5. 在 hello**停用**刀鋒視窗中，系統會提示您確認。 裝置停用是無法復原的「永久性」程序。 您也會收到提醒 tootake 共用/磁碟區離線 hello 主機上。 輸入 hello 裝置名稱 tooconfirm，然後按一下**停用**。
   
    ![](./media/storsimple-virtual-array-failover-dr/failover1.png)
6. 啟動 hello 停用。 Hello 停用作業成功完成之後，您會收到通知。
   
    ![](./media/storsimple-virtual-array-failover-dr/failover2.png)
7. 在 hello 裝置 頁面上，hello 裝置狀態將會立即變更太**Deactivated**。
    ![](./media/storsimple-virtual-array-failover-dr/failover3.png)
8. 在 hello**裝置**刀鋒視窗中，選取並按一下 hello 停用的來源裝置容錯移轉。 
9. 在 hello**裝置儀表板**刀鋒視窗中，按一下 **容錯移轉**。 
10. 在 hello**容錯移轉裝置**刀鋒視窗中，請勿遵循 hello:
    
    1. hello 來源裝置 欄位會自動填入。 請注意 hello 來源裝置 hello 總資料大小。 hello 資料大小應該小於 hello hello 目標裝置上的可用容量。 檢閱 hello hello 來源裝置，例如裝置名稱、 總容量和 hello 的容錯移轉的 hello 共用的名稱與相關聯的詳細資料。

    2. 從可用裝置 hello 下拉式清單中，選擇 **目標裝置**。 僅限 hello 擁有足夠的容量的裝置會顯示在 [hello] 下拉式清單。

    3. 請檢查**我了解這項作業將會容錯移轉資料 toohello 目標裝置**。 

    4. 按一下 [容錯移轉]。
    
        ![](./media/storsimple-virtual-array-failover-dr/failover4.png)
11. 容錯移轉工作起始，您會收到通知。 跳過**裝置 > 工作**toomonitor hello 容錯移轉。
    
     ![](./media/storsimple-virtual-array-failover-dr/failover5.png)
12. 在 hello**作業**刀鋒視窗中，您會看到針對 hello 來源裝置而建立的容錯移轉工作。 此工作會執行 hello DR prechecks。
    
    ![](./media/storsimple-virtual-array-failover-dr/failover6.png)
    
     Hello DR prechecks 成功之後，hello 容錯移轉作業會產生每個共用/磁碟區的來源裝置上的還原作業。
    
    ![](./media/storsimple-virtual-array-failover-dr/failover7.png)
13. Hello 容錯移轉完成，請移 toohello 之後**裝置**刀鋒視窗。
    
    1. 選取並按一下 hello StorSimple 裝置已用來作為 hello hello 容錯移轉程序的目標裝置。
    2. 跳過**設定 > 管理 > 共用**(或**磁碟區**如果 iSCSI 伺服器)。 在 hello**共用**刀鋒視窗中，您可以檢視 hello 舊裝置中所有的 hello 共用 （磁碟區）。
        ![](./media/storsimple-virtual-array-failover-dr/failover9.png)
14. 您必須太[建立 DNS 別名](https://support.microsoft.com/kb/168322)tooconnect，讓所有 hello 嘗試的應用程式可以取得重新導向的 toohello 新裝置。

## <a name="errors-during-dr"></a>DR 期間發生錯誤

**DR 期間雲端連線能力中斷**

DR hello 雲端連線中斷之後是否已啟動並 hello DR hello 裝置還原已經完成之前，將會失敗。 您會收到失敗通知。 DR 的 hello 目標裝置已標示為*無法使用。* 您無法使用 hello 未來 DRs 的相同目標裝置。

**沒有相容的目標裝置**

如果 hello 可用目標裝置沒有足夠的空間，您會看到錯誤 toohello 效果沒有相容的目標裝置。

**前置檢查失敗**

如果沒有符合的 hello prechecks 其中一個，您會看到 precheck 失敗。

## <a name="business-continuity-disaster-recovery-bcdr"></a>業務持續性災害復原 (BCDR)

Hello 整個 Azure 資料中心都停止運作時，就會發生商務持續性災害復原 (BCDR) 案例。 這可能會影響您的 StorSimple 裝置管理員服務與 hello StorSimple 裝置。

如果是在災害發生時之前, 已註冊的 StorSimple 裝置，這些 StorSimple 裝置可能需要刪除 toobe。 Hello 損毀之後, 您可以重新建立並設定這些裝置。

## <a name="next-steps"></a>後續步驟

深入了解如何太[管理使用本機 web UI hello 您 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md)。

