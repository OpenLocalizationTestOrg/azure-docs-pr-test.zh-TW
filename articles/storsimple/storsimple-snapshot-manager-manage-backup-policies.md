---
title: "aaaStorSimple Snapshot Manager 備份原則 |Microsoft 文件"
description: "描述如何 toouse hello StorSimple Snapshot Manager MMC 嵌入式管理單元 toocreate 和管理 hello 控制排定的備份的備份原則。"
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 04415d0b-42f0-4737-8afa-257fb2dbe5d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: c2ae75a8d0568090add6018da18de73eb56e6590
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-backup-policies"></a>使用 StorSimple Snapshot Manager toocreate 及管理備份原則
## <a name="overview"></a>概觀
備份原則會建立在本機或 hello 雲端備份磁碟區資料的排程。 建立備份原則時，您也可以指定保留原則。 (您最多可以保留 64 個快照)。如需備份原則的詳細資訊，請參閱 [StorSimple 8000 系列：混合式雲端解決方案](storsimple-overview.md)中的[備份類型](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies)。

本教學課程說明如何：

* 建立備份原則
* 編輯備份原則
* 刪除備份原則

## <a name="create-a-backup-policy"></a>建立備份原則
使用下列程序 toocreate 新的備份原則的 hello。

#### <a name="toocreate-a-backup-policy"></a>toocreate 備份原則
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。
2. 在 [hello**範圍**] 窗格中，以滑鼠右鍵按一下**備份原則**，按一下**建立備份原則**。

    ![建立備份原則](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    hello**建立原則** 對話方塊隨即出現。

    ![建立原則 - 一般索引標籤](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. 在 hello**一般**索引標籤，完成 hello 下列資訊：

   1. 在 [hello**名稱**] 文字方塊中，輸入 hello 原則的名稱。
   2. 在 hello**磁碟區群組**文字方塊中，型別 hello hello 與 hello 原則相關聯的磁碟區群組名稱。
   3. 選取 [本機快照] 或 [雲端快照]。
   4. 選取快照集 tooretain hello 的數目。 如果您選取**所有**，將會保留 64 個快照 (上限 hello)。
4. 按一下 hello**排程** 索引標籤。

    ![建立原則 - 排程索引標籤](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. 在 hello**排程**索引標籤，完成 hello 下列資訊：

   1. 按一下 hello**啟用**核取方塊 tooschedule hello 下一次備份。
   2. 在 [設定] 之下，選取 [一次]、[每日]、[每週] 或 [每月]。
   3. 在 [hello**啟動**] 文字方塊中，按一下 hello 行事曆圖示，然後選取開始日期。
   4. 在 [ **進階設定**] 之下，您可以設定選用的重複排程和結束日期。
   5. 按一下 [確定] 。

下列資訊的 hello 建立備份原則之後，會出現在 hello**結果**窗格：

* **名稱**– hello 備份原則的名稱。
* **類型**  – 本機快照或雲端快照。
* **磁碟區群組**– hello 與 hello 原則相關聯的磁碟區群組。
* **保留**– hello 保留的快照數目; hello 上限為 64。
* **建立**– 建立此原則的 hello 日期。
* **啟用**– hello 原則目前是否生效： **True**表示它是作用中。**False**表示它不是作用中。

## <a name="edit-a-backup-policy"></a>編輯備份原則
使用下列程序 tooedit 現有的備份原則的 hello。

#### <a name="tooedit-a-backup-policy"></a>tooedit 備份原則
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。
2. 在 [hello**範圍**] 窗格中，按一下 hello**備份原則**節點。 所有的 hello 備份原則會出現在 hello**結果**窗格。
3. 以滑鼠右鍵按一下您想 tooedit，然後再按一下 hello 原則**編輯**。

    ![編輯備份原則](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. 當 hello**建立原則**視窗出現時，請輸入您的變更，然後按一下**確定**。

## <a name="delete-a-backup-policy"></a>刪除備份原則
使用下列程序 toodelete 備份原則的 hello。

#### <a name="toodelete-a-backup-policy"></a>toodelete 備份原則
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。
2. 在 [hello**範圍**] 窗格中，按一下 hello**備份原則**節點。 所有的 hello 備份原則會出現在 hello**結果**窗格。
3. 以滑鼠右鍵按一下您想 toodelete，然後再按一下 hello 備份原則**刪除**。
4. Hello 確認訊息出現時，按一下**是**。

    ![確認刪除備份原則](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a>後續步驟
* 了解如何太[使用您的 StorSimple 解決方案的 StorSimple Snapshot Manager tooadminister](storsimple-snapshot-manager-admin.md)。
* 了解如何太[使用 StorSimple Snapshot Manager tooview 及管理備份工作](storsimple-snapshot-manager-manage-backup-jobs.md)。
