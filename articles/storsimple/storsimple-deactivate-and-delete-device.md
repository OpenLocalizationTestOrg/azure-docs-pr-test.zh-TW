---
title: "aaaDeactivate 和刪除 StorSimple 裝置 |Microsoft 文件"
description: "描述如何從服務，方法是先停用後再將其刪除 tooremove StorSimple 裝置。"
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 155cda38-c5ae-45dc-b7e8-6444494afc9e
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed86bcd089aa957128e14b1709c836d938c131a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-8000-series-device-via-storsimple-manager-service"></a>透過 StorSimple Manager 服務來停用及刪除 StorSimple 8000 系列裝置
## <a name="overview"></a>概觀
您可能會想 tootake 汰 StorSimple 裝置 （例如，如果您要取代或升級您的裝置，或您不再需要使用 StorSimple）。 在 hello 情況下，您將需要 toodeactivate hello 裝置，才能刪除它。 停用伺服器 hello hello 裝置與之間連線 hello 相對應的 StorSimple Manager 服務。 本教學課程說明如何 tooremove StorSimple 裝置的服務，方法是先停用後再將其刪除。 

當您停用裝置時，任何已儲存在本機 hello 裝置的資料將不再可存取。 只會 hello 與 hello 裝置 hello 雲端中儲存相關聯的資料可以復原。  

> [!WARNING]
> 停用是永久性的作業，而且無法復原。 已停用的裝置無法登錄與 hello StorSimple Manager 服務，除非它是第一次重設 toohello 預設原廠設定。 
> 
> hello 原廠重設程序會刪除已儲存在本機裝置的所有 hello 資料。 因此，在您停用裝置之前，您必須擷取所有資料的雲端快照集。 這可讓您 toorecover 所有 hello 資料在後續階段。
> 
> 

本教學課程說明如何：

* 停用的裝置，並刪除 hello 資料
* 停用的裝置並 hello 資料保留

它也會說明如何針對 StorSimple 虛擬裝置來進行停用及刪除作業。

> [!NOTE]
> 您停用 StorSimple 實體或虛擬裝置之前，請確定 toostop 或刪除用戶端和相依於該裝置的主機。
> 
> 

## <a name="deactivate-and-delete-data"></a>停用及刪除資料
如果您想要完全刪除 hello 裝置並不想 tooretain hello 資料 hello 裝置上的，然後完成下列步驟的 hello。

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a>toodeactivate hello 裝置和 delete hello 資料
1. 先前 toodeactivating 裝置，您必須刪除所有 hello 磁碟區容器 （和 hello 磁碟區） 與 hello 裝置相關聯。 只在您刪除相關聯的 hello 備份之後，您可以刪除磁碟區容器。
2. 如下所示停用裝置 hello:
   
   1. Hello StorSimple Manager 服務在**裝置**頁面上，選取 hello 裝置，您想 toodeactivate 並在 hello hello 頁面底部，按一下 **停用**。
   2. 確認訊息隨即出現。 按一下**是**toocontinue。 hello 停用程序將會啟動，並花幾分鐘的時間 toocomplete。
3. 停用之後，您可以完全刪除 hello 裝置。 刪除裝置，即會從裝置連接的 toohello 服務的 hello 清單。 hello 服務可以再管理 hello 刪除裝置。 使用下列步驟 toodelete hello 裝置 hello:
   
   1. 在 hello StorSimple Manager 服務**裝置**頁面上，選取您想 toodelete 停用的裝置。
   2. 在 hello 底部 hello 頁面上，按一下 **刪除**。
   3. 系統將提示您進行確認。 按一下**是**toocontinue。
      
      可能需要幾分鐘，讓 hello 裝置 toobe 刪除。

## <a name="deactivate-and-retain-data"></a>停用並保留資料
如果您有興趣刪除 hello 裝置，但想 tooretain hello 資料，然後完成下列步驟的 hello。

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a>toodeactivate 裝置並 hello 資料保留
1. 停用 hello 裝置。 所有 hello 磁碟區容器，但仍會保留的 hello 裝置 hello 快照集。
   
   1. Hello StorSimple Manager 服務在**裝置**頁面上，選取 hello 裝置，您想 toodeactivate 並在 hello hello 頁面底部，按一下 **停用**。
   2. 確認訊息隨即出現。 按一下**是**toocontinue。 hello 停用程序將會啟動，並花幾分鐘的時間 toocomplete。
2. 您現在可以容錯移轉 hello 磁碟區容器和相關聯的 hello 快照集。 程序，跳過[StorSimple 裝置的容錯移轉和災害復原](storsimple-device-failover-disaster-recovery.md)。
3. 停用和容錯移轉之後, 您可以完全刪除 hello 裝置。 刪除裝置，即會從裝置連接的 toohello 服務的 hello 清單。 hello 服務可以再管理 hello 刪除裝置。 完成下列步驟 toodelete hello 裝置 hello:
   
   1. 在 hello StorSimple Manager 服務**裝置**頁面上，選取您想 toodelete 停用的裝置。
   2. 在 hello 底部 hello 頁面上，按一下 **刪除**。
   3. 系統將提示您進行確認。 按一下**是**toocontinue。
      
      可能需要幾分鐘，讓 hello 裝置 toobe 刪除。

## <a name="deactivate-and-delete-a-virtual-device"></a>停用並刪除虛擬裝置
StorSimple 虛擬裝置，請停用取消配置 hello 虛擬機器。 然後您就可以刪除 hello 虛擬機器及其 hello 資源建立時已佈建。 Hello 虛擬裝置停用之後，它不能還原 tooits 先前的狀態。 

停用產生 hello 下列動作：

* 移除 hello StorSimple 虛擬裝置。
* hello OSDisk 和資料磁碟建立 hello StorSimple 虛擬裝置會移除。
* hello 裝載服務和已佈建期間建立的虛擬網路會保留。 如果您不使用這些項目，就應該手動加以刪除。
* 保留的 hello StorSimple 虛擬裝置所建立的雲端快照集。

## <a name="next-steps"></a>後續步驟
* toorestore hello 停用的裝置 toofactory 預設值、 跳過[hello 裝置 toofactory 預設設定重設](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings)。
* 如需技術協助， [請連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)。
* toolearn 深入了解如何 toouse hello StorSimple Manager 服務移過[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。 

