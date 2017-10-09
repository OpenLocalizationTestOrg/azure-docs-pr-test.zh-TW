---
title: "aaaStorSimple 容錯移轉時，適用於 8000 系列裝置的災害復原 |Microsoft 文件"
description: "深入了解如何 toofail 透過您的 StorSimple 裝置 tooitself、 另一個實體裝置或為雲端應用裝置。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/03/2017
ms.author: alkohli
ms.openlocfilehash: 9d01ee30b15b77072b1d4dfe9a215abc83ffba28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="failover-and-disaster-recovery-for-your-storsimple-8000-series-device"></a>StorSimple 8000 系列裝置的容錯移轉和災害復原

## <a name="overview"></a>概觀

本文說明 hello hello StorSimple 8000 系列裝置的裝置容錯移轉功能，而且如何這項功能可以使用的 toorecover StorSimple 裝置如果發生損毀。 StorSimple 會使用裝置容錯移轉 toomigrate hello 資料從來源裝置 hello datacenter tooanother 目標裝置中。 這篇文章中的 hello 指導方針適用於 tooStorSimple 8000 系列實體裝置和執行軟體版本更新 3 及更新版本的雲端應用裝置。

StorSimple 使用 hello**裝置**刀鋒視窗 toostart hello 裝置容錯移轉功能的嚴重損壞的 hello 事件中。 此刀鋒視窗會列出所有 hello StorSimple 裝置連線的 tooyour StorSimple 裝置管理員服務。

![[裝置] 刀鋒視窗](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)


## <a name="disaster-recovery-dr-and-device-failover"></a>災害復原 (DR) 與裝置容錯移轉

在災害復原 (DR) 案例中，hello 主要裝置會停止運作。 StorSimple 使用 hello 主要裝置當做_來源_並移動 hello 相關聯雲端資料 tooanother_目標_裝置。 此程序為參照的 tooas hello*容錯移轉*。 hello 下列圖形說明容錯移轉的 hello 程序。

![裝置容錯移轉時會發生什麼事？](./media/storsimple-8000-device-failover-disaster-recovery/failover-dr-flow.png)

實體裝置或甚至雲端應用裝置，可能是 hello 容錯移轉的目標裝置。 hello 目標裝置可能會位於相同或不同地理位置 hello 來源裝置 hello。

Hello 容錯移轉期間，您可以選取移轉的磁碟區容器。 StorSimple 會從 hello 來源裝置 toohello 目標裝置，然後變更這些磁碟區容器的 hello 擁有的權。 一旦 hello 磁碟區容器會變更擁有權，StorSimple 從 hello 來源裝置中刪除這些容器。 Hello 刪除完成後，您可以容錯回復 hello 目標裝置。 _容錯回復_傳輸 hello 擁有權後 toohello 原始來源裝置。

### <a name="cloud-snapshot-used-during-device-failover"></a>裝置容錯移轉時使用的雲端快照

下列 DR，hello 最新的雲端備份是使用的 toorestore hello 資料 toohello 目標裝置。 如需有關雲端快照集的詳細資訊，請參閱[使用 hello StorSimple 裝置管理員服務 tootake 手動備份](storsimple-8000-manage-backup-policies-u2.md#take-a-manual-backup)。

在 StorSimple 8000 系列上，備份原則與備份有關係。 如果有多個備份原則的 hello 相同的磁碟區，然後選取 StorSimple hello 與 hello 的磁碟區的最大數目的備份原則。 StorSimple 接著會從選取的 hello 備份原則 toorestore hello 資料 hello 最新備份使用 hello 目標裝置上。

假設有兩個備份原則，defaultPol 與 customPol：

* defaultPol：一個磁碟區 (vol1)，會於每日晚上 10:30 開始執行。
* customPol：四個磁碟區 (vol1、vol2、vol3、vol4)，會於每日晚上 10:00 開始執行。

在此情況下，StorSimple 會針對損毀一致性來排定優先順序，並使用 customPol，因其擁有的磁碟區較多。 hello 於此原則的最新備份是使用的 toorestore 資料。 如需有關如何 toocreate 及管理備份原則，請跳過[使用 hello StorSimple 裝置管理員服務 toomanage 備份原則](storsimple-8000-manage-backup-policies-u2.md)。

## <a name="common-considerations-for-device-failover"></a>裝置容錯移轉的一般注意事項

在您容錯移轉裝置之前，請檢閱下列資訊的 hello:

* 裝置容錯移轉開始前，hello 磁碟區容器內的所有 hello 磁碟區必須都處於離線狀態。 在非計劃性容錯移轉時，StotSimple 磁碟區會自動離線。 但是，如果您正在執行規劃的容錯移轉 (tootest DR)，您必須讓所有 hello 磁碟區離線。
* 只有 hello 具有相關聯的磁碟區容器列出 dr 雲端快照。 必須至少一個磁碟區容器相關聯的雲端快照集 toorecover 資料。
* 如果有跨多個磁碟區容器的複數雲端快照，StorSimple 會將這些磁碟區容器容錯移轉為一個集合。 在極少數的執行個體，跨越多個磁碟區容器的本機快照集，但沒有相關聯的雲端快照集，如果 StorSimple 不容錯移轉 hello 本機快照和 hello 本機資料遺失 DR 之後。
* hello dr 的可用目標裝置是具有足夠的空間 tooaccommodate hello 選定磁碟區容器。 沒有足夠空間的裝置，皆不會列為目標裝置。
* DR （適用於有限的持續時間） 之後, 可能會大幅影響 hello 資料存取效能，為 hello 裝置需要 tooaccess hello hello 雲端的資料並將它儲存在本機。

#### <a name="device-failover-across-software-versions"></a>跨軟體版本的裝置容錯移轉

部署中的 StorSimple 裝置管理員服務可能會有多個實體和雲端裝置，且全都執行不一樣的軟體版本。

使用下列資料表 toodetermine，如果您容錯移轉或失敗後 tooanother 裝置執行不同的軟體版本與 hello 磁碟區類型在 DR 期間的行為方式的 hello。

#### <a name="failover-and-failback-across-software-versions"></a>跨軟體版本的容錯移轉與容錯回復

| 容錯移轉/容錯回復來源 | 實體裝置 | 雲端設備 |
| --- | --- | --- |
| Update 3 tooUpdate 4 |階層式磁碟區以分層的方式進行容錯移轉。 <br></br>本機固定磁碟區以固定在本機的方式進行容錯移轉。 <br></br> 在容錯移轉之後，當您擷取快照 hello Update 4 裝置上[heatmap 式追蹤](storsimple-update4-release-notes.md#whats-new-in-update-4)會介入。 |本機固定磁碟區以分層的方式進行容錯移轉。 |
| 更新 4 tooUpdate 3 |階層式磁碟區以分層的方式進行容錯移轉。 <br></br>本機固定磁碟區以固定在本機的方式進行容錯移轉。 <br></br> 使用備份 toorestore 保留 heatmap 中繼資料。 <br></br>容錯回復後，無法在 Update 3 使用熱度圖式追蹤。 |本機固定磁碟區以分層的方式進行容錯移轉。 |


## <a name="device-failover-scenarios"></a>裝置容錯移轉情節

如果沒有損毀，您可以選擇 toofail 透過 StorSimple 裝置：

* [tooa 實體裝置](storsimple-8000-device-failover-physical-device.md)。
* [tooitself](storsimple-8000-device-failover-same-device.md)。
* [tooa 雲端應用裝置](storsimple-8000-device-failover-cloud-appliance.md)。

hello 上述文件的詳細的步驟的每個提供 hello 上方容錯移轉情況。


## <a name="failback"></a>容錯回復

針對 Update 3 和更新版本，StorSimple 也支援容錯回復。 容錯回復，而且只 hello 反轉的容錯移轉、 hello 目標會變成 hello 來源 hello 原始來源裝置現在 hello 容錯移轉期間會成為 hello 目標裝置。 

容錯回復期間 StorSimple 重新同步處理 hello 資料回復 toohello 主要位置、 中止 hello I/O 與應用程式活動，並轉換後 toohello 原始位置。

完成容錯移轉之後，StorSimple 會執行下列動作的 hello:

* StorSimple 會清除 hello 從 hello 來源裝置容錯移轉的磁碟區容器。
* StorSimple 會初始化背景工作每個磁碟區容器 （容錯） hello 來源裝置上。 如果您嘗試 toofail hello 工作正在進行時，您會收到通知 toothat 效果。 等待 hello 作業完成 toostart hello 容錯回復。
* 採取 toocomplete hello 刪除磁碟區容器的 hello 時間取決於各種因素，例如資料量、 hello 資料、 備份及 hello 可用網路頻寬的數字的 hello 作業的存留期。

如果您正在規劃為容錯移轉或容錯回復進行測試，建議您以含較少資料 (單位為 Gb) 的磁碟區容器進行測試。 通常，您可以啟動 hello 容錯回復 24 小時之後 hello 容錯移轉已完成。

## <a name="frequently-asked-questions"></a>常見問題集

問： **如果 hello DR 失敗或已部分成功，怎樣？**

A. 如果 hello DR 失敗，我們建議您試一次。 hello 第二個裝置容錯移轉作業可感知的 hello hello 第一個作業進度，而且會從該點起開始。

問： **Hello 裝置容錯移轉正在進行時可以刪除裝置嗎？**

A. 您無法在 DR 正在進行時刪除裝置。 Hello DR 完成之後，您只能刪除您的裝置。 您可以監視 hello 裝置容錯移轉作業進行中 hello**作業**刀鋒視窗。

問： **何時沒有 hello 回收啟動 hello 來源裝置上，讓刪除 hello 來源裝置上的本機資料？**

A. 會完全清除 hello 裝置之後，才會啟用 hello 來源裝置記憶體回收。 hello 清理包含清除已容錯移轉從 hello 來源裝置，例如磁碟區、 備份的物件 （而非資料）、 磁碟區容器，以及原則的物件。

問： **如果 hello 刪除 hello hello 來源裝置中的磁碟區容器相關聯的工作，會發生什麼事失敗？**

A.  如果 hello 刪除作業失敗時，您可以手動刪除 hello 磁碟區容器。 在 hello**裝置**刀鋒視窗中，選取 來源裝置，然後按一下**磁碟區容器**。 選取 hello 磁碟區容器，您無法透過和 hello 底部 hello 刀鋒視窗中，按一下**刪除**。 刪除所有 hello 之後 hello 來源裝置上的磁碟區容器容錯移轉，您可以啟動 hello 容錯回復。 如需詳細資訊，請移至太[刪除磁碟區容器](storsimple-8000-manage-volume-containers.md#delete-a-volume-container)。

## <a name="business-continuity-disaster-recovery-bcdr"></a>業務持續性災害復原 (BCDR)

Hello 整個 Azure 資料中心都停止運作時，就會發生商務持續性災害復原 (BCDR) 案例。 這種情況下可能會影響您的 StorSimple 裝置管理員服務與 hello StorSimple 裝置。

如果發生嚴重損壞之前，已登錄 StorSimple 裝置，此裝置可能需要的 tooundergo 原廠重設。 Hello 損毀之後, hello StorSimple 裝置會在顯示 hello Azure 入口網站為離線。 從 hello 入口網站，必須先刪除此裝置。 重設 hello 裝置 toofactory 預設值，並與 hello 服務再重新註冊。

## <a name="next-steps"></a>後續步驟

如果您準備好 tooperform 裝置容錯移轉，請選擇其中一個 hello 下列案例的詳細指示：

- [容錯移轉 tooanother 實體裝置](storsimple-8000-device-failover-physical-device.md)
- [容錯移轉 toohello 相同裝置](storsimple-8000-device-failover-same-device.md)
- [容錯移轉 tooStorSimple 雲端應用裝置](storsimple-8000-device-failover-cloud-appliance.md)

如果您無法透過您的裝置，選擇其中一個 hello 下列選項：

* [停用或刪除 StorSimple 裝置](storsimple-8000-deactivate-and-delete-device.md)。
* [使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。

