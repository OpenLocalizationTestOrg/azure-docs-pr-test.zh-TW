---
title: "aaaStorSimple 容錯移轉時，適用於 8000 系列裝置的災害復原 |Microsoft 文件"
description: "深入了解如何透過您的 StorSimple 裝置 toohello toofail 相同的裝置。"
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
ms.date: 06/23/2017
ms.author: alkohli
ms.openlocfilehash: b0b4216c7af6745ff68b85ca3d655691b43b4334
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-your-storsimple-physical-device-toosame-device"></a>容錯移轉您的 StorSimple 實體裝置 toosame 裝置

## <a name="overview"></a>概觀

如果沒有損毀，本教學課程的描述 hello 步驟需要的 toofail StorSimple 8000 系列實體裝置 tooitself。 StorSimple 會使用 hello 裝置容錯移轉功能 toomigrate 資料來源的實體裝置在 hello datacenter tooanother 實體裝置中。 本教學課程中的 hello 指導方針適用於執行軟體版本更新 3 及更新版本的 tooStorSimple 8000 系列實體裝置。

深入了解裝置容錯移轉和就是從嚴重損毀，使用的 toorecover toolearn 移過[StorSimple 8000 系列裝置的容錯移轉和災害復原](storsimple-8000-device-failover-disaster-recovery.md)。

toofail 透過實體裝置 tooanother 實體裝置，請跳過[相同容錯移轉 toohello StorSimple 實體裝置](storsimple-8000-device-failover-physical-device.md)。 透過 StorSimple 雲端應用裝置，StorSimple 實體裝置 tooa toofail 移過[容錯移轉 tooa StorSimple 雲端應用裝置](storsimple-8000-device-failover-cloud-appliance.md)。


## <a name="prerequisites"></a>必要條件

- 請確定您已檢閱 hello 考量用於裝置容錯移轉。 如需詳細資訊，請移至太[用於裝置容錯移轉的一般考量](storsimple-8000-device-failover-disaster-recovery.md)。


## <a name="steps-toofail-over-toohello-same-device"></a>步驟 toofail toohello 透過相同的裝置

執行下列步驟，若要透過 toohello toofail hello 相同的裝置。

1. 在您的裝置擷取所有 hello 磁碟區的雲端快照。 如需詳細資訊，請移至太[使用 StorSimple 裝置管理員服務 toocreate 備份](storsimple-8000-manage-backup-policies-u2.md)。
2. 重設您的裝置 toofactory 預設值。 請遵循 hello 詳細中的指示[tooreset StorSimple 裝置 toofactory 預設設定的方式](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings)。
3. 移 toohello StorSimple 裝置管理員服務，然後選取**裝置**。 在 hello**裝置**刀鋒視窗中，hello 舊裝置應顯示為**離線**。

    ![來源裝置離線](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. 設定裝置，並再次使用 StorSimple 裝置管理員服務重新註冊裝置。 hello 新註冊的裝置應顯示為**已 tooset 準備註冊**。 hello hello 新裝置的裝置名稱為的 hello 相同 hello 舊裝置但加上數字 tooindicate hello 裝置已重設 toofactory 預設和已註冊一次。

    ![新註冊的裝置準備好 tooset 向上](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. Hello 新裝置，來完成 hello 裝置安裝。 如需詳細資訊，請移至太[步驟 4： 完成基本裝置設定](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup)。 在 hello**裝置**刀鋒視窗中，hello 裝置 hello 狀態變更太**線上**。

   > [!IMPORTANT]
   > **首先，完成 hello 最低設定，或您的 DR 可能會失敗。**

    ![新註冊的裝置狀態為線上](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. 選取 hello 舊裝置 （離線狀態），然後在 hello 命令列中，按一下**容錯移轉**。 在 hello**容錯移轉**刀鋒視窗中，選取舊裝置做為 hello 來源並指定 hello 目標裝置 hello 新註冊的裝置。

    ![容錯移轉摘要](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    如需詳細指示，請參閱太[容錯移轉 tooanother 實體裝置](#fail-over-to-another-physical-device)。

7. 裝置還原作業會建立您可以監視從 hello**作業**刀鋒視窗。

8. Hello 作業已成功完成之後，存取 hello 新裝置，並瀏覽 toohello**磁碟區容器**刀鋒視窗。 請確認所有 hello 磁碟區容器從 hello 舊裝置已都移轉 toohello 新裝置。

   ![移轉磁碟區容器](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. Hello 容錯移轉已完成之後，您可以停用並刪除 hello 入口網站中的 hello 舊裝置。 選取 hello 舊裝置 （離線），以滑鼠右鍵按一下，然後再選取**停用**。 Hello 裝置停用後，會更新 hello 裝置 hello 狀態。

     ![停用來源裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. 選取 hello 停用裝置，以滑鼠右鍵按一下，然後選取**刪除**。 這會從裝置 hello 清單刪除 hello 裝置。

    ![刪除來源裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a>後續步驟

* 在您執行容錯移轉之後，您可能需要過[停用或刪除您的 StorSimple 裝置](storsimple-8000-deactivate-and-delete-device.md)。
* 如需如何 toouse hello StorSimple 裝置管理員服務，請跳過[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。

