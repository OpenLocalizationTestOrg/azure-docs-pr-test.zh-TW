---
title: "aaaDeactivate 及刪除 Microsoft Azure StorSimple Virtual Array |Microsoft 文件"
description: "描述如何從服務，方法是先停用後再將其刪除 tooremove StorSimple 裝置。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: a929f5bc-03e2-4b01-b925-973db236f19f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: b1f3ddb5822d19965739777e238af19b507df984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a>停用及刪除 StorSimple Virtual Array

## <a name="overview"></a>概觀

當您停用 StorSimple Virtual Array 時，您可以中斷 hello hello 裝置與之間連線 hello 相對應的 StorSimple 裝置管理員服務。 本教學課程說明如何：

* 停用裝置 
* 刪除或停用裝置

本文章中的 hello 資訊適用於僅 tooStorSimple 虛擬陣列。 如需 8000 系列的資訊，請 toohow 太[停用或刪除裝置](storsimple-deactivate-and-delete-device.md)。

## <a name="when-toodeactivate"></a>當 toodeactivate 嗎？

停用是永久性的作業，而且無法復原。 您無法以 hello StorSimple 裝置管理員服務重新登錄已停用的裝置。 您可能需要 toodeactivate 並刪除 StorSimple Virtual Array hello 下列案例中：

* **規劃的容錯移轉**： 您的裝置已上線並想 toofail 透過您的裝置。 如果您計劃 tooupgrade tooa 較大的裝置時，您可能需要 toofail 透過您的裝置。 Hello 資料擁有權轉移和 hello 容錯移轉已完成之後，會自動刪除 hello 來源裝置。
* **未規劃的容錯移轉**： 您的裝置已離線，而且您需要 toofail 透過 hello 裝置。 Hello 資料中心中斷，而且您的主要裝置已關閉時，可能會在災害期間發生此情況。 您可以規劃 toofail hello tooa 次要裝置上。 Hello 資料擁有權轉移和 hello 容錯移轉已完成之後，會自動刪除 hello 來源裝置。
* **解除委任**： 想 toodecommission hello 裝置。 這需要 toofirst 停用 hello 裝置，然後再刪除它。 當您停用裝置時，您將無法再存取儲存在本機的任何資料。 您可以儲存在 hello 雲端之唯一存取和復原的 hello 資料。 如果您打算 tookeep hello 裝置資料停用之後，您應該採取所有資料的雲端快照的集之前停用的裝置。 此雲端快照可讓您 toorecover 所有 hello 資料在後續階段。

## <a name="deactivate-a-device"></a>停用裝置

toodeactivate 您的裝置，執行下列步驟的 hello。

#### <a name="toodeactivate-hello-device"></a>toodeactivate hello 裝置

1. 在您的服務，請移過**管理 > 裝置**。 在 hello**裝置**刀鋒視窗，按一下，然後選取 hello 裝置，您會希望 toodeactivate。
   
    ![選取裝置 toodeactivate](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. 在您**裝置儀表板**刀鋒視窗中，按一下 [ **...多個**hello] 清單中，從選取**停用**。
   
    ![按一下停用](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. 在 hello**停用**刀鋒視窗中，型別 hello 裝置名稱，然後按一下**停用**。 
   
    ![確認停用](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    hello 停用程序會啟動並在幾分鐘的時間 toocomplete。
   
    ![停用進行中](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. 停用之後，重新整理裝置 hello 清單。
   
    ![停用完成](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    您現在可以刪除此裝置。

## <a name="delete-hello-device"></a>刪除裝置 hello

裝置有 toobe 第一個已停用的 toodelete 它。 刪除裝置，即會從裝置連接的 toohello 服務的 hello 清單。 hello 服務可以再管理 hello 刪除裝置。 不過與 hello 裝置相關聯的 hello 資料會維持 hello 雲端。 所以這項資料會累算費用。

toodelete hello 裝置，請執行下列步驟的 hello。

#### <a name="toodelete-hello-device"></a>toodelete hello 裝置

1. 在您 StorSimple 裝置管理員 」 中，跳過**管理 > 裝置**。 在 hello**裝置**刀鋒視窗中，選取您想 toodelete 停用的裝置。
2. 在 hello**裝置儀表板**刀鋒視窗中，按一下  **...多個**，然後按一下**刪除**。
   
   ![選取裝置 toodelete](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. 在 hello**刪除**刀鋒視窗中，輸入 hello 名稱，您的裝置 tooconfirm hello 刪除然後再按一下**刪除**。 正在刪除 hello 裝置不會刪除 hello 與 hello 裝置相關聯的雲端資料。 
   
   ![Confirm delete](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. hello 刪除啟動，並採用幾分鐘的時間 toocomplete。
   
   ![刪除進行中](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    刪除 hello 裝置之後，您可以檢視裝置 hello 更新清單。

## <a name="next-steps"></a>後續步驟

* 如需詳細資訊，透過 toofail 移過[容錯移轉和災害復原您的 StorSimple Virtual Array](storsimple-virtual-array-failover-dr.md)。

* toolearn 深入了解如何 toouse hello StorSimple 裝置管理員服務移過[使用 hello StorSimple 裝置管理員服務 tooadminister 您 StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md)。 

