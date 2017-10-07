---
title: "aaaStorSimple 容錯移轉和災害復原 |Microsoft 文件"
description: "深入了解如何 toofail 透過您的 StorSimple 裝置 tooitself、 另一個實體裝置或虛擬裝置。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5751598e-49c8-42b3-8121-fea5857a7d83
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/16/2016
ms.author: alkohli
ms.openlocfilehash: 00ce365f8a9095d1f0292e665d7f9eaa844b44ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="failover-and-disaster-recovery-for-your-storsimple-device"></a>StorSimple 裝置的容錯移轉與災害復原
## <a name="overview"></a>概觀
本教學課程描述 hello 步驟需要的 toofail 透過 StorSimple 裝置 hello 災害事件中。 在容錯移轉可讓您 toomigrate 您的資料來源中的裝置 hello datacenter tooanother 實體或虛擬裝置位於 hello 相同或不同的地理位置。 

災害復原 (DR) 進行協調，透過 hello 裝置容錯移轉功能，並起始從 hello**裝置**頁面。 此頁面會製為表格所有 hello StorSimple 裝置連線的 tooyour StorSimple Manager 服務。 每個裝置 hello 易記名稱、 狀態、 已佈建和最大容量，會顯示型別和模型。

![[裝置] 頁面](./media/storsimple-device-failover-disaster-recovery/IC740972.png)

本教學課程中的 hello 指導方針會套用在所有的軟體版本之間 tooStorSimple 實體和虛擬裝置。

## <a name="disaster-recovery-dr-and-device-failover"></a>災害復原 (DR) 與裝置容錯移轉
在災害復原 (DR) 案例中，hello 主要裝置會停止運作。 在此情況下，您可以移動 hello 使用 hello 主要裝置當做 hello 與 hello 失敗的裝置 tooanother 裝置相關聯的雲端資料*來源*並指定另一個裝置當做 hello*目標*。 您可以選取一個或多個磁碟區容器 toomigrate toohello 目標裝置。 此程序為參照的 tooas hello*容錯移轉*。 

Hello 容錯移轉期間 hello 來源裝置 hello 磁碟區容器變更擁有權，而且傳送的 toohello 目標裝置。 一旦 hello 磁碟區容器會變更擁有權，這些會刪除從 hello 來源裝置。 Hello 刪除完成後，然後可以回失敗 hello 目標裝置。

通常會遵循 DR、 hello 最新的備份是使用的 toorestore hello 資料 toohello 目標裝置。 但是如果有多個備份原則 hello 相同的磁碟區，然後取得挑選 hello 與 hello 的磁碟區的最大數目的備份原則，而且 hello 該原則的最新備份 hello 目標裝置上的使用的 toorestore hello 資料。

例如，如果有兩個的備份原則 （一個預設值和一個自訂） *defaultPol*， *customPol*以 hello 下列詳細資料：

* defaultPol︰一個磁碟區 (vol1) 會於每日下午 10:30 開始執行。
* customPol︰四個磁碟區 (vol1、vol2、vol3、vol4) 會於每日下午 10:00 開始執行。

在此情況下，將會使用 customPol  ，因為它有更多磁碟區，而我們會針對損毀一致性排定優先順序。 hello 於此原則的最新備份是使用的 toorestore 資料。

## <a name="considerations-for-device-failover"></a>裝置容錯移轉考量
在 hello 事件中的嚴重損壞，您可以選擇透過您的 StorSimple 裝置的 toofail:

* tooa 實體裝置 
* tooitself
* tooa 虛擬裝置

任何裝置容錯移轉，請記得 hello 下列：

* hello DR 的必要條件是 hello 磁碟區容器內的所有 hello 磁碟區都已離線而且 hello 磁碟區容器具有相關聯的雲端快照集。 
* hello dr 的可用目標裝置是具有足夠的空間 tooaccommodate hello 選定磁碟區容器。 
* hello 裝置所連接的 tooyour 服務但不是符合足夠 hello 準則將無法當做目標裝置的可用空間。
* 下列 DR，有限的時間，可能會大幅影響 hello 資料存取效能，為 hello 裝置會需要 tooaccess hello hello 雲端的資料並將它儲存在本機。

#### <a name="device-failover-across-software-versions"></a>跨軟體版本的裝置容錯移轉
部署中的 StorSimple Manager 服務可能會有多個實體和虛擬裝置，且全都執行不一樣的軟體版本。 Hello 軟體版本而定，hello hello 裝置上的磁碟區類型可能也會不同。 例如，執行 Update 2 或更高版本的裝置會有固定在本機的磁碟區和分層磁碟區 (包含做為分層子集的封存)。 更新前 2 裝置 hello 上可能有分層另一方面和封存磁碟區。 

使用下列資料表 toodetermine，如果您可以容錯移轉在 DR 期間執行的磁碟區類型不同的軟體版本與 hello 行為 tooanother 裝置 hello。

| 容錯移轉自 | 允許實體裝置 | 允許虛擬裝置 |
| --- | --- | --- |
| Update 2 toopre-Update 1 （版本，0.1，0.2，0.3） |否 |否 |
| Update 2 tooUpdate 1 （1、 1.1、 1.2） |是 <br></br>如果使用本機固定或分層磁碟區或混合的兩個磁碟區永遠為容錯移轉的 hello 分層。 |是<br></br>如果使用固定在本機的磁碟區，這些會容錯移轉為分層磁碟區。 |
| Update 2 tooUpdate 2 （較新版本） |是<br></br>如果使用本機固定或分層磁碟區或兩個混合，hello 磁碟區會一律容錯移轉為 hello 啟動磁碟區類型。固定在本機，分層為階層式和固定在本機。 |是<br></br>如果使用固定在本機的磁碟區，這些會容錯移轉為分層磁碟區。 |

#### <a name="partial-failover-across-software-versions"></a>跨軟體版本的部分容錯移轉
如果您想 tooperform 部分的容錯移轉使用 StorSimple 來源裝置執行更新前 1 tooa 執行 Update 1 或更新版本為目標，請遵循本指南。 

| 部分容錯移轉從 | 允許實體裝置 | 允許虛擬裝置 |
| --- | --- | --- |
| 更新 1 （版本，0.1，0.2，0.3） 前 tooUpdate 1 或更新版本 |[是]，請參閱下面的 hello 最佳作法是提示。 |[是]，請參閱下面的 hello 最佳作法是提示。 |

> [!TIP]
> Update 1 及更新版本中的雲端中繼資料和資料格式已變更。 因此，我們不建議部分的容錯移轉，從更新前 1 tooUpdate 1 或更新版本。 如果您需要 tooperform 部分的容錯移轉時，我們建議您先套用 Update 1 或更新版本上的兩部 hello 裝置 （來源和目標），並再繼續 hello 容錯移轉。 
> 
> 

## <a name="fail-over-tooanother-physical-device"></a>容錯移轉 tooanother 實體裝置
執行下列步驟 toorestore hello 裝置 tooa 目標實體裝置。

1. 請確認您想 toofail 透過 hello 磁碟區容器具有相關聯的雲端快照。
2. 在 [hello**裝置**頁面上，按一下 hello**磁碟區容器**] 索引標籤。
3. 選取您想要 toofail tooanother 裝置上的磁碟區容器。 按一下 hello 磁碟區容器 toodisplay hello 清單內這個容器的磁碟區。 選取磁碟區，然後按一下**離線**tootake hello 磁碟區離線。 Hello 磁碟區容器中的所有 hello 磁碟區都重複此程序。
4. Hello 重複上一個步驟的所有 hello 磁碟區容器想 toofail tooanother 裝置上。
5. 在 hello**裝置**頁面上，按一下**容錯移轉**。
6. 在 hello 開啟精靈，在**透過選擇磁碟區容器 toofail**:
   
   1. Hello 清單中的磁碟區容器，選取您希望透過 toofail hello 磁碟區容器。
      **只有 hello 與相關聯的雲端快照集磁碟區容器，並且顯示離線的磁碟區。**
   2. 在下**選擇目標裝置**hello 選取容器中的 hello 磁碟區，請從可用裝置 hello 下拉式清單中選取的目標裝置。 只有具有可用容量的 hello hello 裝置會顯示 hello 下拉式清單中。
   3. 最後，檢閱下的所有 hello 容錯移轉設定**確認容錯移轉**。 按一下核取圖示，hello![核取圖示](./media/storsimple-device-failover-disaster-recovery/IC740895.png)。
7. 容錯移轉工作會建立，可監視透過 hello**作業**頁面。 如果您容錯移轉的 hello 磁碟區容器有本機磁碟區，您會看到每個本機磁碟區 （不適用於分層磁碟區） hello 容器中的個別還原作業。 這些還原作業可能需要一段時間 toocomplete。 它很可能稍早完成該 hello 容錯移轉工作。 請注意，這些磁碟區將本機保證只有 hello 還原作業完成之後執行。 Hello 容錯移轉完成之後，請繼續 toohello**裝置**頁面。                                            
   
   1. 選取 hello 裝置已用來作為 hello hello 容錯移轉程序的目標裝置。
   2. 移 toohello**磁碟區容器**頁面。 應該會列出所有 hello 磁碟區容器以及舊裝置 hello 中的 hello 磁碟區。

## <a name="failover-using-a-single-device"></a>使用單一裝置容錯移轉
執行下列步驟，如果您只有單一裝置與需要 tooperform 容錯移轉的 hello。

1. 在您的裝置擷取所有 hello 磁碟區的雲端快照。
2. 重設您的裝置 toofactory 預設值。 請遵循 hello 詳細中的指示[tooreset StorSimple 裝置 toofactory 預設設定的方式](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings)。
3. 設定裝置並再次向 StorSimple Manager 服務註冊。
4. 在 hello**裝置**hello 舊裝置應顯示為頁面上，**離線**。 hello 新註冊的裝置應顯示為**線上**。
5. Hello 新裝置，請先完成 hello hello 裝置的最小的設定。 
   
   > [!IMPORTANT]
   > **Hello 最低設定尚未完成第一次，如果您的 DR 將會失敗結果 hello 目前實作中的 bug。未來版本中將會修正這個問題。**
   > 
   > 
6. 選取 hello 舊裝置 （離線狀態），然後按一下**容錯移轉**。 在顯示 hello 精靈中，容錯移轉這個裝置並指定 hello 目標裝置 hello 新註冊的裝置。 如需詳細指示，請參閱太[容錯移轉 tooanother 實體裝置](#fail-over-to-another-physical-device)。
7. 裝置還原作業將會建立您可以監視從 hello**作業**頁面。
8. Hello 作業已成功完成之後，存取 hello 新裝置，並瀏覽 toohello**磁碟區容器**頁面。 所有 hello 磁碟區容器從 hello 舊裝置現在都應該已移轉的 toohello 新裝置。

## <a name="fail-over-tooa-storsimple-virtual-device"></a>容錯移轉 tooa StorSimple 虛擬裝置
您必須擁有的 StorSimple 虛擬裝置建立及設定先前 toorunning 此程序。 如果執行 Update 2，請考慮使用 hello DR 中具有 64 TB，並使用進階儲存體 8020 虛擬裝置。 

執行下列步驟 toorestore hello tooa 目標 StorSimple 虛擬裝置 hello。

1. 請確認您想 toofail 透過 hello 磁碟區容器具有相關聯的雲端快照。
2. 在 [hello**裝置**頁面上，按一下 hello**磁碟區容器**] 索引標籤。
3. 選取您想要 toofail tooanother 裝置上的磁碟區容器。 按一下 hello 磁碟區容器 toodisplay hello 清單內這個容器的磁碟區。 選取磁碟區，然後按一下**離線**tootake hello 磁碟區離線。 Hello 磁碟區容器中的所有 hello 磁碟區都重複此程序。
4. Hello 重複上一個步驟的所有 hello 磁碟區容器想 toofail tooanother 裝置上。
5. 在 hello**裝置**頁面上，按一下**容錯移轉**。
6. 在 hello 開啟精靈，在**選擇磁碟區容器 toofailover**，完成下列 hello:
   
    a. Hello 清單中的磁碟區容器，選取您希望透過 toofail hello 磁碟區容器。
   
    **只有 hello 與相關聯的雲端快照集磁碟區容器，並且顯示離線的磁碟區。**
   
    b. 在下**hello 選取容器中選擇目標裝置 hello 磁碟區**，選取 hello StorSimple 虛擬裝置，從可用裝置 hello 下拉式清單。 **僅限 hello 擁有足夠的容量的裝置會顯示 hello 下拉式清單中。**  
7. 最後，檢閱下的所有 hello 容錯移轉設定**確認容錯移轉**。 按一下核取圖示，hello![核取圖示](./media/storsimple-device-failover-disaster-recovery/IC740895.png)。
8. Hello 容錯移轉完成之後，請繼續 toohello**裝置**頁面。
   
    a. 選取 hello StorSimple 虛擬裝置已用來作為 hello hello 容錯移轉程序的目標裝置。
   
    b. 移 toohello**磁碟區容器**頁面。 現在應該會列出所有的 hello 磁碟區容器，以及 hello 舊裝置中的 hello 磁碟區。

![提供的影片](./media/storsimple-device-failover-disaster-recovery/Video_icon.png) **提供的影片**

toowatch 的視訊示範如何還原失敗透過實體裝置 tooa 虛擬裝置 hello 雲端中，按一下[這裡](https://azure.microsoft.com/documentation/videos/storsimple-and-disaster-recovery/)。

## <a name="failback"></a>容錯回復
針對 Update 3 和更新版本，StorSimple 也支援容錯回復。 Hello 容錯移轉已完成之後，hello 執行下列動作：

* hello 容錯移轉的磁碟區容器會清除從 hello 來源裝置。
* Hello 來源裝置上起始背景工作每個磁碟區容器 （容錯移轉）。 如果您嘗試 toofailback hello 作業正在進行時，您會收到通知 toothat 效果。 您必須 toowait hello 作業之前完成 toostart hello 容錯回復。 
  
    hello 時間 toocomplete hello 刪除磁碟區容器會相依於各種因素，例如資料量、 hello 資料、 備份及 hello 可用網路頻寬的數字的 hello 作業的存留期。 如果您正在規劃測試容錯移轉/容錯回復，建議您以含較少資料 (單位為 Gb) 的磁碟區容器進行測試。 在大部分情況下，您可以啟動 hello 容錯回復 24 小時之後 hello 容錯移轉已完成。 

## <a name="frequently-asked-questions"></a>常見問題集
問： **如果 hello DR 失敗或已部分成功，怎樣？**

A. 如果 hello DR 失敗，我們建議您試一次。 hello，第二次 DR 知道所有已完成，而且當 hello 程序會停止 hello 第一次。 hello DR 程序會從該點開始及更新版本。 

問： **Hello 裝置容錯移轉正在進行時可以刪除裝置嗎？**

A. 您無法在 DR 正在進行時刪除裝置。 Hello DR 完成之後，您只能刪除您的裝置。

問：    **何時沒有 hello 回收啟動 hello 來源裝置上，讓刪除 hello 來源裝置上的本機資料？**

A. Hello 裝置完全清除之後，才會在 hello 來源裝置上啟用回收。 hello 清理包含清除已容錯移轉從 hello 來源裝置，例如磁碟區、 備份的物件 （而非資料）、 磁碟區容器，以及原則的物件。

問： **如果 hello 刪除 hello hello 來源裝置中的磁碟區容器相關聯的工作，會發生什麼事失敗？**

A.  Hello 刪除作業失敗時，如果您將需要 toomanually 觸發程序 hello 刪除 hello 磁碟區容器。 在 hello**裝置**頁面上，選取 來源裝置，然後按一下**磁碟區容器**。 選取 hello 磁碟區容器，您無法透過和 hello hello 頁面底部按一下**刪除**。 一旦您已刪除所有 hello hello 來源裝置上的磁碟區容器容錯移轉，您可以啟動 hello 容錯回復。

## <a name="business-continuity-disaster-recovery-bcdr"></a>業務持續性災害復原 (BCDR)
Hello 整個 Azure 資料中心都停止運作時，就會發生商務持續性災害復原 (BCDR) 案例。 這可能會影響您的 StorSimple Manager 服務與 hello StorSimple 裝置。

如果是在災害發生時之前, 已註冊的 StorSimple 裝置，這些 StorSimple 裝置可能需要的 tooundergo 原廠重設。 Hello 損毀之後, hello StorSimple 裝置會顯示為離線。 hello 入口網站，必須先刪除 hello StorSimple 裝置，然後原廠重設應完成，後面接著重新註冊。

## <a name="next-steps"></a>後續步驟
* 在您執行容錯移轉之後，您可能需要過[停用或刪除您的 StorSimple 裝置](storsimple-deactivate-and-delete-device.md)。
* 如需如何 toouse hello StorSimple Manager 服務，請跳過[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。

