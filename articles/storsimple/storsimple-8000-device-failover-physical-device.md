---
title: "aaaStorSimple 容錯移轉，災害復原 tooa StorSimple 8000 系列實體裝置 |Microsoft 文件"
description: "深入了解如何 toofail 透過 StorSimple 8000 系列實體裝置 tooanother 實體裝置。"
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
ms.openlocfilehash: 29d2576a96c446ff5ffcd98dcd0f5a07f1ab08ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooa-storsimple-8000-series-physical-device"></a>容錯移轉 tooa StorSimple 8000 系列實體裝置

## <a name="overview"></a>概觀

如果沒有損毀，本教學課程的描述 hello 步驟需要的 toofail StorSimple 8000 系列實體裝置 tooanother StorSimple 實體裝置。 StorSimple 會使用 hello 裝置容錯移轉功能 toomigrate 資料來源的實體裝置在 hello datacenter tooanother 實體裝置中。 本教學課程中的 hello 指導方針適用於執行軟體版本更新 3 及更新版本的 tooStorSimple 8000 系列實體裝置。

深入了解裝置容錯移轉和就是從嚴重損毀，使用的 toorecover toolearn 移過[StorSimple 8000 系列裝置的容錯移轉和災害復原](storsimple-8000-device-failover-disaster-recovery.md)。

透過 StorSimple 雲端應用裝置，StorSimple 實體裝置 tooa toofail 移過[容錯移轉 tooa StorSimple 雲端應用裝置](storsimple-8000-device-failover-cloud-appliance.md)。 透過實體裝置 tooitself，toofail 移過[相同容錯移轉 toohello StorSimple 實體裝置](storsimple-8000-device-failover-same-device.md)。


## <a name="prerequisites"></a>必要條件

- 請確定您已檢閱 hello 考量用於裝置容錯移轉。 如需詳細資訊，請移至太[用於裝置容錯移轉的一般考量](storsimple-8000-device-failover-disaster-recovery.md)。

- 您必須在 StorSimple 8000 系列實體裝置 hello datacenter 中部署。 hello 裝置必須執行 Update 3 或更新的軟體版本。 如需詳細資訊，請移至太[部署在內部部署 StorSimple 裝置](storsimple-8000-deployment-walkthrough-u2.md)。


## <a name="steps-toofail-over-tooa-physical-device"></a>透過 tooa 實體裝置的步驟 toofail

執行下列步驟 toorestore hello 裝置 tooa 目標實體裝置。

1. 請確認您想 toofail 透過 hello 磁碟區容器具有相關聯的雲端快照。 如需詳細資訊，請移至太[使用 StorSimple 裝置管理員服務 toocreate 備份](storsimple-8000-manage-backup-policies-u2.md)。
2. 在 tooyour StorSimple 裝置管理員 的 **裝置**。 在 hello**裝置**刀鋒視窗、 移 toohello 清單與您的服務連接的裝置。
    ![選取裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)
3. 選取並按一下您的來源裝置。 hello 來源裝置沒有您想 toofail 透過的 hello 磁碟區容器。 跳過**設定 > 磁碟區容器**。
4. 選取您想要 toofail tooanother 裝置上的磁碟區容器。 按一下 hello 磁碟區容器 toodisplay hello 清單內這個容器的磁碟區。 選取磁碟區，按一下滑鼠右鍵，然後按一下**離線**tootake hello 磁碟區離線。 Hello 磁碟區容器中的所有 hello 磁碟區都重複此程序。
5. Hello 重複上一個步驟的所有 hello 磁碟區容器想 toofail tooanother 裝置上。
6. 返回 toohello**裝置**刀鋒視窗。 在 hello 命令列中，按一下**容錯移轉**。
    按一下 [容錯移轉]![](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev2.png)
    
7. 在 hello**容錯移轉**刀鋒視窗中，執行下列步驟的 hello:
   
   1. 按一下 [來源]。 會顯示 hello 與雲端快照集的相關聯的磁碟區的磁碟區容器。 只顯示 hello 容器是可進行容錯移轉。 Hello 清單中的磁碟區容器，選取您希望透過 toofail hello 磁碟區容器。 **只有 hello 與相關聯的雲端快照集磁碟區容器，並且顯示離線的磁碟區。**

       ![選取來源](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev5.png)
   2. 按一下 [目標]。 Hello hello 先前步驟中選取的磁碟區容器，請從可用裝置 hello 下拉式清單中選取的目標裝置。 只有 hello 裝置具有足夠的容量 tooaccommodate 來源磁碟區容器會顯示在 [hello] 清單。

        ![選取目標](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev6.png)

   3. 最後，檢閱下的所有 hello 容錯移轉設定**摘要**。 您已檢閱 hello 設定之後，選取 [hello] 核取方塊，指出選取的磁碟區容器中的 hello 磁碟區會離線。 按一下 [確定] 。

       ![檢閱容錯移轉設定](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev8.png)
  
8. StorSimple 會建立容錯移轉作業。 按一下 hello 工作通知 toomonitor hello 容錯移轉工作透過 hello**作業**刀鋒視窗。

    如果您容錯移轉的 hello 磁碟區容器有本機磁碟區，您會看到每個本機磁碟區 （不適用於分層磁碟區） hello 容器中的個別還原作業。 這些還原作業可能需要一段時間 toocomplete。 它很可能稍早完成該 hello 容錯移轉工作。 只 hello 還原作業完成之後，這些磁碟區會有本機保證。

    ![監視容錯移轉作業](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

9. Hello 容錯移轉完成之後，請繼續 toohello**裝置**刀鋒視窗。
   
   1. 選取 hello 裝置已用來作為 hello hello 容錯移轉程序的目標裝置。

       ![選取裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

   2. 移 toohello**磁碟區容器**刀鋒視窗。 應該會列出所有 hello 磁碟區容器以及舊裝置 hello 中的 hello 磁碟區。

       ![檢視目標磁碟區容器](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev16.png)


## <a name="next-steps"></a>後續步驟

* 在您執行容錯移轉之後，您可能需要過[停用或刪除您的 StorSimple 裝置](storsimple-8000-deactivate-and-delete-device.md)。
* 如需如何 toouse hello StorSimple 裝置管理員服務，請跳過[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。

