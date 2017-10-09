---
title: "aaaStorSimple 容錯移轉，災害復原 tooa StorSimple 雲端應用裝置 |Microsoft 文件"
description: "了解如何透過您的 StorSimple 8000 系列實體裝置 tooa toofail 雲端應用裝置。"
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: e8a0bca057024358e3a557fe85a42ddefea36cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooyour-storsimple-cloud-appliance"></a>容錯移轉 tooyour StorSimple 雲端應用裝置

## <a name="overview"></a>概觀

如果沒有損毀，本教學課程的描述 hello 步驟需要的 toofail StorSimple 8000 系列實體裝置 tooa StorSimple 雲端應用裝置。 StorSimple 會使用 hello 裝置容錯移轉功能 toomigrate 資料來源的實體裝置在 hello datacenter tooa 雲端應用裝置在 Azure 中執行。 本教學課程中的 hello 指導方針適用於 tooStorSimple 8000 系列實體裝置和執行軟體版本更新 3 及更新版本的雲端應用裝置。

深入了解裝置容錯移轉和就是從嚴重損毀，使用的 toorecover toolearn 移過[StorSimple 8000 系列裝置的容錯移轉和災害復原](storsimple-8000-device-failover-disaster-recovery.md)。

透過 StorSimple 實體裝置 tooanother 實體裝置，toofail 移過[容錯移轉 tooa StorSimple 實體裝置](storsimple-8000-device-failover-physical-device.md)。 透過裝置 tooitself，toofail 移過[相同容錯移轉 toohello StorSimple 實體裝置](storsimple-8000-device-failover-same-device.md)。

## <a name="prerequisites"></a>必要條件

- 請確定您已檢閱 hello 考量用於裝置容錯移轉。 如需詳細資訊，請移至太[用於裝置容錯移轉的一般考量](storsimple-8000-device-failover-disaster-recovery.md)。

- 執行此程序之前，您必須已建立並設定 StorSimple 雲端設備。 如果執行更新 3 的軟體版本或更新版本中，請考慮使用 8020 雲端應用裝置 hello DR。 hello 8020 模型具有 64 TB，並使用進階儲存體。 如需詳細資訊，請移至太[部署和管理 StorSimple 雲端應用裝置](storsimple-8000-cloud-appliance-u2.md)。

## <a name="steps-toofail-over-tooa-cloud-appliance"></a>步驟 toofail 透過 tooa 雲端應用裝置

執行下列步驟 toorestore hello 裝置 tooa 目標 StorSimple 雲端應用裝置 hello。

1.  請確認您想 toofail 透過 hello 磁碟區容器具有相關聯的雲端快照。 如需詳細資訊，請移至太[使用 StorSimple 裝置管理員服務 toocreate 備份](storsimple-8000-manage-backup-policies-u2.md)。
2. 移 tooyour StorSimple 裝置管理員服務，然後按一下**裝置**。 在 hello**裝置**刀鋒視窗、 移 toohello 清單與您的服務連接的裝置。
    ![選取裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)
3. 選取並按一下您的來源裝置。 hello 來源裝置沒有您想 toofail 透過的 hello 磁碟區容器。 跳過**設定 > 磁碟區容器**。

    ![選取裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. 選取您想要 toofail tooanother 裝置上的磁碟區容器。 按一下 hello 磁碟區容器 toodisplay hello 清單內這個容器的磁碟區。 選取磁碟區，按一下滑鼠右鍵，然後按一下**離線**tootake hello 磁碟區離線。

    ![選取裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. Hello 磁碟區容器中的所有 hello 磁碟區都重複此程序。

     ![選取裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. Hello 重複上一個步驟的所有 hello 磁碟區容器想 toofail tooanother 裝置上。

7. 返回 toohello**裝置**刀鋒視窗。 在 hello 命令列中，按一下**容錯移轉**。

    ![按一下 [容錯移轉]](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. 在 hello**容錯移轉**刀鋒視窗中，執行下列步驟的 hello:
   
    1. 按一下 [來源]。 透過選取 hello 磁碟區容器 toofail。 **只有 hello 與相關聯的雲端快照集磁碟區容器，並且顯示離線的磁碟區。**
        ![選取來源](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)
    2. 按一下 [目標]。 從可用的裝置 hello 下拉式清單中選取目標雲端應用裝置。 **只有 hello 裝置具有足夠的容量 tooaccommodate 來源磁碟區容器會顯示在 [hello] 清單。**

        ![選取目標](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. 檢閱下方的 hello 容錯移轉設定**摘要**並選取 [hello] 核取方塊，指出選取的磁碟區容器中的 hello 磁碟區會離線。 

        ![檢閱容錯移轉設定](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. 已建立容錯移轉作業。 toomonitor hello 容錯移轉作業中，按一下 hello 工作通知。

    ![監視容錯移轉作業](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. Hello 容錯移轉完成之後，請回到 toohello**裝置**刀鋒視窗。

    1. 選取已作為 hello 目標 hello 容錯移轉的 hello 裝置。

       ![選取裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. 按一下 [磁碟區容器]。 應該會列出所有 hello 磁碟區容器以及舊裝置 hello 中的 hello 磁碟區。

       如果 hello 容錯移轉的磁碟區容器具有本機固定磁碟區，這些磁碟區無法透過與分層磁碟區。 StorSimple 雲端設備不支援已固定在本機的磁碟區。

       ![檢視目標磁碟區容器](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a>後續步驟

* 在您執行容錯移轉之後，您可能需要過[停用或刪除您的 StorSimple 裝置](storsimple-8000-deactivate-and-delete-device.md)。

* 如需如何 toouse hello StorSimple 裝置管理員服務，請跳過[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。

