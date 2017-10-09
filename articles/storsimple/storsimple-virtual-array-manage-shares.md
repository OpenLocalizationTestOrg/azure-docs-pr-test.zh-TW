---
title: "aaaManage StorSimple Virtual Array 共用 |Microsoft 文件"
description: "描述 hello StorSimple 裝置管理員，並說明如何 toouse 它在您的 StorSimple Virtual Array toomanage 共用。"
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: 0a799c83-fde5-4f3f-af0e-67535d1882b6
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 9b57d7ec7c0b7de5a22e1b816daa8852d0f32a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-shares-on-hello-storsimple-virtual-array"></a>在 hello StorSimple Virtual Array 上使用 hello StorSimple 裝置管理員服務 toomanage 共用

## <a name="overview"></a>概觀

本教學課程將說明 toouse hello StorSimple 裝置管理員服務 toocreate 並管理您的 StorSimple Virtual Array 上的共用。

hello StorSimple 裝置管理員服務是 hello Azure 入口網站，可讓您從單一 web 介面來管理您的 StorSimple 解決方案中的延伸模組。 在加法 toomanaging 共用和磁碟區中，您可以使用 hello StorSimple 裝置管理員服務 tooview 和管理裝置、 檢視警示、 管理備份原則，以及管理 hello 備份類別目錄。

## <a name="share-types"></a>共用類型

StorSimple 共用可以是︰

* **固定在本機**： 一直 hello 陣列上這些共用中的資料，並不 spill toohello 雲端。
* **分層**： 這些共用中的資料可以 spill toohello 雲端。 當您建立階層式的共用時，大約 10%的 hello 空間 hello 本機層上佈建和 90%的 hello 空間 hello 雲端中佈建。 例如，如果您佈建 1 TB 共用、 100 GB，也可以位於 hello 本機空間和 900GB 會用在 hello 雲端時 hello 資料層。 這會表示，如果您在 hello 裝置上執行所有 hello 的本機空間不足，無法佈建階層式的共用 （因為 hello 10%上需要有本機 hello 層將無法使用）。

### <a name="provisioned-capacity"></a>佈建的容量

請參閱下表針對每個共用類型的最大佈建的容量 toohello。

| **限制識別碼** | **限制** |
| --- | --- |
| 分層共用的大小下限 |500 GB |
| 分層共用的大小上限 |20 TB |
| 固定在本機的共用的大小下限 |50 GB |
| 固定在本機的共用的大小上限 |2 TB |

## <a name="hello-shares-blade"></a>hello 共用刀鋒視窗

hello**共用**您 StorSimple 服務摘要 刀鋒視窗的功能表顯示 hello 存放裝置共用指定的 StorSimple 陣列上，並可讓您 toomanage 它們。

![[共用] 刀鋒視窗](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

共用包含一系列屬性：

* **共用名稱**-必須是唯一的且有助於識別 hello 共用的描述性名稱。
* **狀態** – 可為連線或離線。 如果共用離線，hello 共用的使用者不會無法 tooaccess 它。
* **型別**– 指出是否 hello 共用**分層**(hello 預設) 或**固定在本機**。
* **容量**– 指定 hello 做為比較的 toohello 可以儲存在 hello 共用的資料量總計的資料數量。
* **描述**– 選擇性的設定，可協助說明 hello 共用。
* **權限**-hello NTFS 權限 toohello 共用可以透過 Windows 檔案總管 進行管理。
* **備份**– 以防的 hello StorSimple Virtual Array，所有共用會自動都啟用備份。

![共用的詳細資料](./media/storsimple-virtual-array-manage-shares/share-details.png)

使用 hello 指示在本教學課程 tooperform hello，下列工作：

* 新增共用
* 修改共用
* 讓共用離線
* 刪除共用

## <a name="add-a-share"></a>新增共用

1. 從 hello StorSimple 服務摘要刀鋒視窗中，按一下  **+ 新增共用**hello 命令列。 這會開啟 hello**新增共用**刀鋒視窗。

    ![新增共用](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. 在 hello**新增共用**刀鋒視窗中，請勿遵循 hello:
   
    1. 在 hello**共用名稱**欄位中，輸入您共用的唯一名稱。 hello 名稱必須是包含 3 too127 個字元的字串。

    2. 選擇性**描述**hello 共用。 hello 描述可協助識別 hello 共用擁有者。

    3. 在 hello**類型**下拉式清單中，指定是否 toocreate**分層**或**固定在本機**共用。 對於需要本機保證、低延遲，以及高效能的工作負載，請選取 [固定在本機的共用] 。 對於所有其他資料，請選取 [階層式] 共用。

    4. 在 hello**容量**欄位中，指定 hello 共用的 hello 大小。 階層式共用必須介於 500 GB 和 20 TB 之間，而固定在本機的共用必須介於 50 GB 和 2 TB 之間。

    5. 在 hello**設為預設的完整權限**欄位中，指派 toohello hello 權限的使用者或正在存取此共用的 hello 群組。 指定 hello hello 使用者或群組的名稱 hello 使用者在 _john@contoso.com_ 格式。 我們建議您使用使用者群組 （而非單一使用者） tooallow 系統管理員權限 tooaccess 這些共用。 您已指派 hello 權限之後，您可以使用檔案總管 toomodify 這些權限。
3. 共用設定完成之後，按一下 [建立]。 將指定的 hello 與建立的共用設定，您會看到通知。 根據預設，備份將會啟用 hello 共用。
4. hello 共用的 tooconfirm 已成功建立，請移 toohello**共用**刀鋒視窗。 您應該會看到共用列出 hello。
   
    ![共用建立成功](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a>修改共用

當您需要 toochange hello 描述 hello 共用時，請修改共用。 建立 hello 共用之後，就可以修改其他的共用屬性。

#### <a name="toomodify-a-share"></a>toomodify 共用

1. 從 hello**共用**設定 hello StorSimple 服務摘要 刀鋒視窗上，選取 hello 的 hello toomodify 希望您的共用所在的虛擬陣列。
2. **選取**hello 共用 tooview hello 目前描述，並加以修改。
3. 儲存您的變更，依序按一下 hello**儲存**命令列。 將會套用您指定的設定，您會看到通知。
   
    ![ 編輯共用](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a>讓共用離線

您可能需要 tootake 的共用離線，當您計劃 toomodify 它或刪除它。 當共用已離線時，即無法進行讀寫存取。 您將需要 tootake hello 共用離線 hello 裝置以及 hello 主機上。

#### <a name="tootake-a-share-offline"></a>tootake 的共用離線

1. 請確定有問題該 hello 共用不是使用中，再將其離線。
2. 藉由執行下列步驟的 hello hello 陣列離線採用 hello 共用：
   
    1. 從 hello**共用**設定 hello StorSimple 服務摘要 刀鋒視窗上，選取 hello 的 hello tootake 離線希望您的共用所在的虛擬陣列。

    2. **選取**hello 共用，然後按一下**...** （或者以滑鼠右鍵按一下此資料列中），然後從 hello 內容功能表中，選取**離線**。
     
        ![離線共用](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. 檢閱在 hello hello 資訊**離線**刀鋒視窗，並確認您接受 hello 作業。 按一下**離線**tootake hello 共用離線。 您會看到 hello 作業正在進行中的通知。

    4. hello 共用的 tooconfirm 已成功取得離線，請移 toohello**共用**刀鋒視窗。 您應該會看到 hello hello 共用為離線狀態。

## <a name="delete-a-share"></a>刪除共用

> [!IMPORTANT]
> 只有已離線的共用才能刪除。


完成下列步驟 toodelete 共用 hello。

#### <a name="toodelete-a-share"></a>toodelete 共用

1. 從 hello**共用**設定 hello StorSimple 服務摘要 刀鋒視窗上，選取 hello 您想在哪一個 hello 共用 toodelete 所在的虛擬陣列。
2. **選取**hello 共用，然後按一下**...** （或者以滑鼠右鍵按一下此資料列中），然後從 hello 內容功能表中，選取**刪除**。
   
    ![刪除共用](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. 檢查 hello 狀態要 toodelete hello 共用。 如果您想要 toodelete hello 共用未離線，先使其離線。 中的 hello 步驟[離線工作共用](#take-a-share-offline)。
4. 當系統提示您確認在 hello**刪除**刀鋒視窗中，接受 hello 確認，然後按一下 **刪除**。 hello 共用現在將會刪除與 hello**共用**刀鋒視窗會顯示 hello 虛擬陣列中的共用 hello 更新清單。

## <a name="next-steps"></a>後續步驟
了解如何太[複製 StorSimple 共用](storsimple-virtual-array-clone.md)。

