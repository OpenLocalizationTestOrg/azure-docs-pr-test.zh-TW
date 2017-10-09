---
title: "在 StorSimple Virtual Array aaaManage 磁碟區 |Microsoft 文件"
description: "描述 hello StorSimple 裝置管理員，並說明如何 toouse 它 toomanage StorSimple 虛擬陣列上的磁碟區。"
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: caa6a26b-b7ba-4a05-b092-1a79450225cf
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 46aa6d7508b3e62f75a3b78ed73302b88320a0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-service-toomanage-volumes-on-hello-storsimple-virtual-array"></a>使用 StorSimple 裝置管理員服務 toomanage 磁碟區上 hello StorSimple Virtual Array

## <a name="overview"></a>概觀

本教學課程將說明 toouse hello StorSimple 裝置管理員服務 toocreate 並管理您的 StorSimple 虛擬陣列上的磁碟區。

hello StorSimple 裝置管理員服務是 hello Azure 入口網站，可讓您從單一 web 介面來管理您的 StorSimple 解決方案中的延伸模組。 在加法 toomanaging 共用和磁碟區中，您可以使用 hello StorSimple 裝置管理員服務 tooview 和管理裝置、 檢視警示，以及檢視和管理備份原則與 hello 備份類別目錄。

## <a name="volume-types"></a>磁碟區類型

StorSimple 磁碟區可以是：

* **固定在本機**： 一直 hello 陣列上這些磁碟區中的資料，並不 spill toohello 雲端。
* **分層**： 這些磁碟區中的資料可以 spill toohello 雲端。 當您建立階層式磁碟區時，大約 10%的 hello 空間 hello 本機層上佈建和 90%的 hello 空間 hello 雲端中佈建。 例如，如果您佈建 1 TB 磁碟區、 100 GB，也可以位於 hello 本機空間和 900GB 會用在 hello 雲端時 hello 資料層。 這會表示，如果您在 hello 裝置上執行所有 hello 的本機空間不足，無法佈建分層磁碟區 （因為 hello 10%上需要有本機 hello 層將無法使用）。

### <a name="provisioned-capacity"></a>佈建的容量
請參閱下表針對每個磁碟區類型的最大佈建的容量 toohello。

| **限制識別碼**                                       | **限制**     |
|------------------------------------------------------------|---------------|
| 分層磁碟區的大小下限                            | 500 GB        |
| 分層磁碟區的大小上限                            | 5 TB          |
| 固定在本機的磁碟區的大小下限                    | 50 GB         |
| 固定在本機的磁碟區的大小上限                    | 500 GB        |

## <a name="hello-volumes-blade"></a>hello 磁碟區 刀鋒視窗
hello**磁碟區**您 StorSimple 服務摘要 刀鋒視窗的功能表顯示 hello 存放磁碟區上指定的 StorSimple 陣列，並可讓您 toomanage 它們。

![[磁碟區] 刀鋒視窗](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

磁碟區是由一系列屬性所組成：

* **磁碟區名稱**– 描述性的名稱必須是唯一的可協助識別 hello 磁碟區。
* **狀態** – 可為連線或離線。 如果磁碟區已離線，就不允許存取 toouse hello 磁碟區的可見 tooinitiators （伺服器）。
* **型別**– 指出 hello 磁碟區是否為**分層**(hello 預設) 或**固定在本機**。
* **容量**– 指定 hello 做為比較的 toohello 的 hello 啟動器 （伺服器） 來儲存的資料量總計的資料數量。
* **備份**– 以防 hello StorSimple Virtual Array 的所有磁碟區會自動啟用備份。
* **連線主機**– 指定允許存取 toothis 磁碟區的 hello 啟動器 （伺服器）。

![磁碟區詳細資料](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

使用 hello 指示在本教學課程 tooperform hello，下列工作：

* 新增磁碟區
* 修改磁碟區
* 使磁碟區離線
* 刪除磁碟區

## <a name="add-a-volume"></a>新增磁碟區

1. 從 hello StorSimple 服務摘要刀鋒視窗中，按一下 **新增磁碟區 +** hello 命令列。 這會開啟 hello**新增磁碟區**刀鋒視窗。
   
    ![新增磁碟區](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. 在 hello**新增磁碟區**刀鋒視窗中，請勿遵循 hello:
   
   * 在 hello**磁碟區名稱**欄位中，輸入您的磁碟區的唯一名稱。 hello 名稱必須是包含 3 too127 個字元的字串。
   * 在 hello**類型**下拉式清單中，指定是否 toocreate**分層**或**固定在本機**磁碟區。 對於需要本機保證、低延遲及更高效能的工作負載，請選取 [固定在本機的磁碟區]。 針對所有其他資料，請選取 [階層式] 磁碟區。
   * 在 hello**容量**欄位中，指定 hello hello 磁碟區的大小。 階層式磁碟區必須介於 500 GB 和 5 TB 之間，而固定在本機的磁碟區必須介於 50 GB 和 500 GB 之間。
   * * 按一下**連線主機**，選取 存取控制記錄 (ACR) 對應 toohello iSCSI 啟動器您想 tooconnect toothis 磁碟區，然後再按一下**選取**。
3. tooadd 新連線的主機，按一下**新增**，輸入的名稱 hello 主機和其 iSCSI 合格名稱 (IQN)，然後按一下**新增**。
   
    ![新增磁碟區](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. 磁碟區設定完成之後，按一下 [建立]。 將指定的 hello 與建立磁碟區設定，您會看到在 hello 成功建立 hello 相同的通知。 依預設會啟用 hello 磁碟區備份。
5. hello 磁碟區的 tooconfirm 已成功建立，請移 toohello**磁碟區**刀鋒視窗。 您應該會看到列出的 hello 磁碟區。
   
    ![磁碟區建立成功](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a>修改磁碟區

當您需要存取 hello 的磁碟區的 toochange hello 主機時，請修改磁碟區。 hello 磁碟區的其他屬性，即無法修改已建立 hello 磁碟區。

#### <a name="toomodify-a-volume"></a>toomodify 磁碟區

1. 從 hello**磁碟區**設定 hello StorSimple 服務摘要 刀鋒視窗上，選取 hello 的 hello toomodify 希望您的磁碟區所在的虛擬陣列。
2. **選取**hello 磁碟區，然後按一下**連線主機**tooview hello 目前連線的主機，並加以修改 tooa 不同的伺服器。
   
    ![編輯磁碟區](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. 儲存您的變更，依序按一下 hello**儲存**命令列。 將會套用您指定的設定，您會看到通知。

## <a name="take-a-volume-offline"></a>使磁碟區離線

您可能需要 tootake 磁碟區離線，當您計劃 toomodify 它或刪除它。 當磁碟區離線時，即無法進行讀寫存取。 您將需要 tootake hello 磁碟區離線 hello 裝置以及 hello 主機上。

#### <a name="tootake-a-volume-offline"></a>tootake 磁碟區離線

1. 請確定有問題的 hello 磁碟區不是使用中，再將其離線。
2. Hello 主機上的 hello 磁碟區離線讓第一次。 這可免除 hello 磁碟區上的資料損毀的任何潛在風險。 如需特定步驟，請參閱主機作業系統的 toohello 指示。
3. Hello hello 主機上的磁碟區離線後，採用的 hello 陣列離線 hello 磁碟區，藉由執行下列步驟的 hello:
   
   * 從 hello**磁碟區**設定 hello StorSimple 服務摘要 刀鋒視窗上，選取 hello 的 hello 您想 tootake 離線的磁碟區所在的虛擬陣列。
   * **選取**hello 磁碟區，然後按一下**...** （或者以滑鼠右鍵按一下此資料列中），然後從 hello 內容功能表中，選取**離線**。
     
        ![讓磁碟區離線](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * 檢閱在 hello hello 資訊**離線**刀鋒視窗，並確認您接受 hello 作業。 按一下**離線**tootake hello 磁碟區離線。 您會看到 hello 作業正在進行中的通知。
   * hello 磁碟區已成功地使其離線的 tooconfirm 移 toohello**磁碟區**刀鋒視窗。 您應該會看到 hello hello 磁碟區狀態為離線。
     
       ![確認磁碟區離線](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a>刪除磁碟區

> [!IMPORTANT]
> 只有當磁碟區離線時，您才能予以刪除。
> 
> 

完成下列步驟 toodelete 磁碟區的 hello。

#### <a name="toodelete-a-volume"></a>toodelete 磁碟區

1. 從 hello**磁碟區**設定 hello StorSimple 服務摘要 刀鋒視窗上，選取 hello 的 hello toodelete 希望您的磁碟區所在的虛擬陣列。
2. **選取**hello 磁碟區，然後按一下**...** （或者以滑鼠右鍵按一下此資料列中），然後從 hello 內容功能表中，選取**刪除**。
   
    ![刪除磁碟區](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. 檢查 hello 狀態想 toodelete hello 磁碟區。 如果您想要 toodelete hello 磁碟區未離線，使其離線的第一個步驟，下列 hello 步驟[使磁碟區離線](#take-a-volume-offline)。
4. 當系統提示您確認在 hello**刪除**刀鋒視窗中，接受 hello 確認，然後按一下 **刪除**。 hello 磁碟區現在將會刪除與 hello**磁碟區**刀鋒視窗會顯示更新的 hello hello 虛擬陣列中的磁碟區清單。

## <a name="next-steps"></a>後續步驟

了解如何太[複製 StorSimple 磁碟區](storsimple-virtual-array-clone.md)。

