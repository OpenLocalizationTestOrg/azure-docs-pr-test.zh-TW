---
title: "aaaDeactivate 和刪除 StorSimple 8000 系列裝置 |Microsoft 文件"
description: "描述如何從服務，方法是先停用後再將其刪除 tooremove StorSimple 裝置。"
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
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 841ecd7f0fb5e425bf23e1fe0044faeab2af4b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-device"></a>停用及刪除 StorSimple 裝置

## <a name="overview"></a>概觀

本文說明如何 toodeactivate 並刪除已連接的 tooa StorSimple 裝置管理員服務的 StorSimple 裝置。 這篇文章中的 hello 指導方針適用於只有 tooStorSimple 8000 系列裝置包括 hello StorSimple 雲端應用程式。 如果您使用 StorSimple Virtual Array，然後跳過[停用及刪除 StorSimple Virtual Array](storsimple-virtual-array-deactivate-and-delete-device.md)。

停用伺服器 hello hello 裝置與之間連線 hello 相對應的 StorSimple 裝置管理員服務。 您可能會想 tootake 汰 StorSimple 裝置 （例如，如果您要取代或升級您的裝置，或您不再需要使用 StorSimple）。 如果是這樣，您需要 toodeactivate hello 裝置，才能刪除它。

當您停用裝置時，已無法存取任何已儲存在本機 hello 裝置的資料。 只會 hello 與 hello 裝置 hello 雲端中儲存相關聯的資料可以復原。

> [!WARNING]
> 停用是永久性的作業，而且無法復原。 已停用的裝置無法登錄以 hello StorSimple 裝置管理員服務，除非它是重設 toofactory 預設值。
>
> hello 原廠重設程序會刪除已儲存在本機裝置的所有 hello 資料。 因此，在您停用裝置之前，您必須擷取所有資料的雲端快照。 此雲端快照可讓您 toorecover 所有 hello 資料在後續階段。

閱讀本教學課程之後，您將能夠：

* 停用的裝置，並刪除 hello 資料。
* 停用的裝置，並保留 hello 資料。

> [!NOTE]
> 在您停用 StorSimple 實體裝置或雲端設備之前，請停止或刪除相依於該裝置的用戶端和主機。


## <a name="deactivate-and-delete-data"></a>停用及刪除資料

如果您想要完全刪除 hello 裝置並不想 tooretain hello 資料 hello 裝置上的，然後完成下列步驟的 hello。

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a>toodeactivate hello 裝置和 delete hello 資料

1. 停用裝置之前，您必須刪除所有 hello 磁碟區容器 （和 hello 磁碟區） 與 hello 裝置相關聯。 只在您刪除相關聯的 hello 備份之後，您可以刪除磁碟區容器。

    > [!NOTE]
    > 您停用 StorSimple 實體裝置或雲端應用裝置之前，請確定從 hello 裝置會實際刪除 hello hello 刪除磁碟區容器中的資料。 您可以監視 hello 雲端耗用量圖表，以及當您看見 hello 雲端使用量卸除，因為已刪除的 hello 備份，則可繼續 toodeactivate hello 裝置。 如果您停用之前的 hello 裝置此下拉式清單就會發生，hello 資料困在 hello 儲存體帳戶和累算費用。

2. 如下所示停用裝置 hello:
   
   1. 移 tooyour StorSimple 裝置管理員服務，然後按一下**裝置**。 在 hello**裝置**刀鋒視窗中，選取 hello 裝置 toodeactivate、 按一下滑鼠右鍵，然後再按一下您想**停用**。

        ![停用 StorSimple 裝置](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. 在 hello**停用**刀鋒視窗中，輸入 hello 裝置名稱 tooconfirm，然後按一下**停用**。 hello 停用程序會啟動並在幾分鐘的時間 toocomplete。

        ![停用 StorSimple 裝置](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)

3. 停用之後，您可以完全刪除 hello 裝置。 刪除裝置，即會從裝置連接的 toohello 服務的 hello 清單。 hello 服務可以再管理 hello 刪除裝置。 使用下列步驟 toodelete hello 裝置 hello:
   
   1. 移 tooyour StorSimple 裝置管理員服務，然後按一下**裝置**。 在 hello**裝置**刀鋒視窗中，選取 hello 停用裝置 toodelete、 按一下滑鼠右鍵，然後再按一下您想**刪除**。

        ![停用 StorSimple 裝置](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. 在 hello**刪除**刀鋒視窗中，輸入 hello 裝置名稱 tooconfirm，然後按一下**刪除**。 hello 可能需要幾分鐘的時間 toocomplete。

        ![停用 StorSimple 裝置](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. 已成功完成 hello 刪除之後，您會收到通知。 hello 裝置清單也會更新 tooreflect hello 刪除。

## <a name="deactivate-and-retain-data"></a>停用並保留資料

如果您有興趣刪除 hello 裝置，但想 tooretain hello 資料，然後完成下列步驟的 hello:

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a>toodeactivate 裝置並 hello 資料保留
1. 停用 hello 裝置。 所有 hello 磁碟區容器和的 hello 裝置 hello 快照集會保留。
   
   1. 移 tooyour StorSimple 裝置管理員服務，然後按一下**裝置**。 在 hello**裝置**刀鋒視窗中，選取 hello 裝置 toodeactivate、 按一下滑鼠右鍵，然後再按一下您想**停用**。

         ![停用 StorSimple 裝置](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. 在 hello**停用**刀鋒視窗中，輸入 hello 裝置名稱 tooconfirm，然後按一下**停用**。 hello 停用程序會啟動並在幾分鐘的時間 toocomplete。

         ![停用 StorSimple 裝置](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)
2. 您現在可以容錯移轉 hello 磁碟區容器和相關聯的 hello 快照集。 程序，跳過[StorSimple 裝置的容錯移轉和災害復原](storsimple-8000-device-failover-disaster-recovery.md)。
3. 停用和容錯移轉之後, 您可以完全刪除 hello 裝置。 刪除裝置，即會從裝置連接的 toohello 服務的 hello 清單。 hello 服務可以再管理 hello 刪除裝置。 完成下列步驟的 hello toodelete hello 裝置：
   
   1. 移 tooyour StorSimple 裝置管理員服務，然後按一下**裝置**。 在 hello**裝置**刀鋒視窗中，選取 hello 停用裝置 toodelete、 按一下滑鼠右鍵，然後再按一下您想**刪除**。

       ![停用 StorSimple 裝置](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. 在 hello**刪除**刀鋒視窗中，輸入 hello 裝置名稱 tooconfirm，然後按一下**刪除**。 hello 可能需要幾分鐘的時間 toocomplete。

       ![停用 StorSimple 裝置](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. 已成功完成 hello 刪除之後，您會收到通知。 hello 裝置清單也會更新 tooreflect hello 刪除。

     
## <a name="deactivate-and-delete-a-cloud-appliance"></a>停用及刪除雲端設備

為 StorSimple 雲端應用裝置中，從 hello 入口網站停用取消配置，並刪除 hello 虛擬機器，與 hello 資源建立時已佈建。 Hello 雲端應用裝置已停用之後，它不能還原 tooits 先前的狀態。

![停用 StorSimple 雲端設備](./media/storsimple-8000-deactivate-and-delete-device/deactivate7.png)

停用產生 hello 下列動作：

* hello StorSimple 雲端應用裝置會從 hello 服務移除。
* 刪除 hello hello StorSimple 雲端應用裝置的虛擬機器。
* hello OS 磁碟和資料磁碟建立 hello StorSimple 雲端應用裝置會移除。
* 保留 hello 裝載服務和已佈建期間建立的虛擬網路。 如果您不使用這些項目，就應該手動加以刪除。
* 會保留 hello StorSimple 雲端應用裝置所建立的雲端快照。

Hello 雲端應用裝置已停用之後，您可以從裝置 hello 清單中刪除它。 選取 hello 停用裝置，以滑鼠右鍵按一下，然後按一下**刪除**。 StorSimple 通知您一旦 hello 裝置會刪除與 hello 裝置更新的清單。

## <a name="next-steps"></a>後續步驟

* toorestore hello 停用的裝置 toofactory 預設值、 跳過[hello 裝置 toofactory 預設設定重設](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings)。
* 如需技術協助， [請連絡 Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md)。
* toolearn 深入了解如何 toouse hello StorSimple 裝置管理員服務移過[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。

