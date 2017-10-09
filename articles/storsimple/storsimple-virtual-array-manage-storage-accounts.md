---
title: "aaaManage StorSimple Virtual Array 儲存體帳戶認證 |Microsoft 文件"
description: "說明如何使用 hello StorSimple 裝置管理員 設定頁面 tooadd、 編輯、 刪除或旋轉 hello 安全性金鑰 hello StorSimple Virtual Array 相關聯的儲存體帳戶認證。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 234bf8bb-d5fe-40be-9d25-721d7482bc3b
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.openlocfilehash: 22a0341eae0b89020065be4dbfaae77999f8be0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-storage-account-credentials-for-storsimple-virtual-array"></a>使用 StorSimple 裝置管理員 toomanage StorSimple Virtual Array 的儲存體帳戶認證

## <a name="overview"></a>概觀
hello**組態**hello StorSimple 裝置管理員服務刀鋒視窗，您的 StorSimple Virtual Array 的區段提供可由 hello StorSimple Manager 服務的 hello 全域服務參數。 這些參數可以是裝置連線 toohello 服務，並包含套用的 tooall hello:

* 儲存體帳戶認證
* 存取控制記錄
  
  ![裝置管理員服務儀表板](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccts-dashboard.png)  

本教學課程說明如何新增、編輯或刪除 StorSimple Virtual Array 的儲存體帳戶認證。 本教學課程中的 hello 資訊僅適用於 toohello StorSimple Virtual Array。 如需 toomanage 儲存體帳戶中 8000 系列的如何資訊，請參閱[使用 hello StorSimple Manager 服務 toomanage 儲存體帳戶](storsimple-manage-storage-accounts.md)。

儲存體帳戶認證都包含 hello 裝置 hello 認證使用 tooaccess 儲存體帳戶與您的雲端服務提供者。 Microsoft Azure 儲存體帳戶，這些是認證，例如 hello 帳戶名稱和 hello 主要存取金鑰。

在 hello**儲存體帳戶認證**刀鋒視窗中，建立 hello 計費訂用帳戶的認證會包含下列資訊的 hello 以表格格式顯示所有儲存體帳戶：

* **名稱**– hello 指派唯一名稱 toohello 帳戶建立時。
* **啟用 SSL** – 是否 hello 啟用 SSL，所以裝置到雲端的通訊都會透過 hello 安全通道。
  
  ![[設定] 區段](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccountcredentials-blade.png)

hello 最常見的工作相關 toostorage 帳戶認證，可對 hello**儲存體帳戶認證**刀鋒視窗會：

* 新增儲存體帳戶認證
* 編輯儲存體帳戶認證
* 刪除儲存體帳戶認證

## <a name="types-of-storage-account-credentials"></a>儲存體帳戶認證的類型
有三種儲存體帳戶認證類型可以與 StorSimple 裝置搭配使用。

* **自動產生的儲存體帳戶認證**– 第一次建立 hello 服務時，就 hello 名所示，自動產生這種類型的儲存體帳戶認證。 toolearn 深入了解如何建立這個儲存體帳戶認證，請參閱[建立新的服務](storsimple-virtual-array-manage-service.md#create-a-service)。
* **hello 服務訂用帳戶中的儲存體帳戶認證**– 這些是 hello Azure 儲存體帳戶相關聯的認證 hello 相同訂用帳戶的 hello 服務。 toolearn 深入了解如何建立這些儲存體帳戶認證，請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。
* **hello 服務訂用帳戶以外的儲存體帳戶認證**-這些是與您的服務沒有關聯的 hello Azure 儲存體帳戶認證，並可能存在於之前 hello 服務已建立。

## <a name="add-a-storage-account-credential"></a>新增儲存體帳戶認證
您可以加入儲存體帳戶認證 tooyour StorSimple 裝置管理員服務組態，藉由提供唯一的易記名稱和存取認證連結 toohello 儲存體帳戶。 您也可以啟用您的裝置與 hello 雲端之間的網路通訊的安全通道 hello 安全通訊端層 (SSL) 模式 toocreate hello 選項。

您可以為指定的雲端服務提供者建立多個帳戶。 正在儲存 hello 儲存體帳戶認證，而 hello 服務會嘗試 toocommunicate 與您的雲端服務提供者。 此時會進行驗證 hello 認證和您所提供的 hello 存取資料。 只有當 hello 驗證成功時，會建立儲存體帳戶認證。 Hello 驗證失敗時，會顯示適當的錯誤訊息。

使用下列程序 tooadd Azure 儲存體帳戶認證的 hello:

* 儲存體帳戶認證具有 tooadd hello 相同 Azure 訂用帳戶 hello 裝置管理員服務
* tooadd 超出 hello 裝置管理員服務訂用帳戶的 Azure 儲存體帳戶認證

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a>儲存體帳戶認證具有 tooadd hello 相同 Azure 訂用帳戶 hello 裝置管理員服務

1. 瀏覽 tooyour 裝置管理員服務，選取，然後按兩下。 這會開啟 hello**概觀**刀鋒視窗。
2. 選取**儲存體帳戶認證**內 hello**組態**> 一節。
3. 按一下 [新增] 。
4. 在 hello**加入儲存體帳戶**刀鋒視窗中，請勿遵循 hello:
   
    1. 在 [訂用帳戶] 中，選取 [目前]。
    2. 提供 hello Azure 儲存體帳戶名稱。
    3. 選取**啟用**toocreate StorSimple 裝置與 hello 雲端之間的網路通訊的安全通道。 只有當您在私人雲端內操作時，才選取 [停用]。
    4. 按一下 [新增] 。 已成功建立 hello 儲存體帳戶之後，您會收到通知。<br></br>
   
        ![新增現有儲存體帳戶認證](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

#### <a name="tooadd-an-azure-storage-account-credential-that-is-outside-of-hello-device-manager-service-subscription"></a>tooadd 超出 hello 裝置管理員服務訂用帳戶的 Azure 儲存體帳戶認證

1. 瀏覽 tooyour 裝置管理員服務，選取，然後按兩下。 這會開啟 hello**概觀**刀鋒視窗。
2. 選取**儲存體帳戶認證**內 hello**組態**> 一節。 這樣就會列出任何現有儲存體帳戶的認證與 hello StorSimple 裝置管理員服務相關聯。
3. 按一下 [新增] 。
4. 在 hello**加入儲存體帳戶**刀鋒視窗中，請勿遵循 hello:
   
    1. 在 [訂用帳戶] 中，選取 [其他]。
   
    2. 提供您的 Azure 儲存體帳戶認證 hello 名稱。
   
    3. 在 [hello**儲存體帳戶存取金鑰**] 文字方塊中，提供 hello 您的 Azure 儲存體帳戶認證的主要存取金鑰。 tooget 此索引鍵，移 toohello Azure 儲存體服務，選取您的儲存體帳戶認證，然後按一下**管理的帳戶金鑰**。 您現在可以複製 hello 主要存取金鑰。
   
    4. tooenable SSL，按一下 hello**啟用**按鈕 toocreate StorSimple 裝置管理員服務和 hello 雲端之間的網路通訊的安全通道。 按一下 hello**停用**按鈕只有當您在私人雲端內操作。
   
    5. 按一下 [新增] 。 已成功建立 hello 儲存體帳戶認證之後，您會收到通知。

5. 底下的 hello StorSimple 設定裝置管理員服務刀鋒視窗上會顯示 hello 新建立的儲存體帳戶認證**儲存體帳戶認證**。
   
    ![新增外部 hello 裝置管理員服務訂用帳戶的儲存體帳戶認證](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-outside-storageacct.png)

## <a name="edit-a-storage-account-credential"></a>編輯儲存體帳戶認證
您可以編輯裝置所使用的儲存體帳戶認證。 如果您編輯目前正在使用儲存體帳戶認證，hello 欄位可用 toomodify 而 hello 便捷鍵 hello 儲存體帳戶認證的 hello SSL 模式。 您可以提供 hello 新儲存體存取金鑰，或修改 hello**啟用 SSL 模式**選取項目並儲存更新的 hello 的設定。

#### <a name="tooedit-a-storage-account-credential"></a>tooedit 儲存體帳戶認證
1. 瀏覽 tooyour 裝置管理員服務，選取，然後按兩下。 這會開啟 hello**概觀**刀鋒視窗。
2. 選取**儲存體帳戶認證**內 hello**組態**> 一節。 這樣就會列出任何現有儲存體帳戶的認證與 hello StorSimple 裝置管理員服務相關聯。
3. 在 hello 表格式清單中的儲存體帳戶認證，請選取，然後按兩下您想 toomodify hello 帳戶。
4. 在 hello 儲存體帳戶認證**屬性**刀鋒視窗中，請勿遵循 hello:
   
   1. 如果有必要，您可以修改 hello**啟用 SSL**模式選取項目。
   2. 您可以選擇 tooregenerate 儲存體帳戶認證的存取金鑰。 如需詳細資訊，請參閱[hello 儲存體帳戶金鑰重新產生](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys)。 提供 hello 新儲存體帳戶認證金鑰。 Azure 儲存體帳戶時，這是 hello 主要存取金鑰。
   3. 按一下**儲存**頂端的 hello hello**屬性**刀鋒視窗 toosave hello 設定。 hello 設定會更新在 hello**儲存體帳戶認證**刀鋒視窗。
      
      ![編輯儲存體帳戶認證](./media/storsimple-virtual-array-manage-storage-accounts/ova-edit-storageacct.png)

## <a name="delete-a-storage-account-credential"></a>刪除儲存體帳戶認證
> [!IMPORTANT]
> 您只能刪除非使用中的儲存體帳戶認證。 如果您要刪除的儲存體帳戶認證正在使用中，系統會通知您。
> 
> 

#### <a name="toodelete-a-storage-account-credential"></a>toodelete 儲存體帳戶認證
1. 瀏覽 tooyour 裝置管理員服務，選取，然後按兩下。 這會開啟 hello**概觀**刀鋒視窗。
2. 選取**儲存體帳戶認證**內 hello**組態**> 一節。 這樣就會列出任何現有儲存體帳戶的認證與 hello StorSimple 裝置管理員服務相關聯。
3. 在 hello 表格式清單中的儲存體帳戶認證，請選取，然後按兩下您想 toodelete hello 帳戶。
4. 在 hello 儲存體帳戶認證**屬性**刀鋒視窗中，請勿遵循 hello:
   
   1. 按一下**刪除**toodelete hello 認證。
   2. 當提示確認，請按一下**是**toocontinue 與 hello 刪除。 hello 表格清單已更新的 tooreflect hello 變更。
      
      ![刪除儲存體帳戶認證](./media/storsimple-virtual-array-manage-storage-accounts/ova-del-storageacct.png)

## <a name="synchronizing-storage-account-credential-keys"></a>同步處理儲存體帳戶認證金鑰
基於安全性理由，通常是在資料中心內才需要替換金鑰。 Microsoft Azure 系統管理員可以重新產生，或直接存取 hello 儲存體帳戶認證 （透過 hello Microsoft Azure 儲存體服務)，以變更 hello 主要或次要金鑰。 hello StorSimple 裝置 Manager 服務不會自動看到這項變更。

tooinform hello StorSimple 裝置管理員 hello 變更的服務，您需要 tooaccess hello StorSimple 裝置管理員服務，存取 hello 儲存體帳戶認證，然後再同步處理 hello 主要或次要金鑰 （視何者有所變更）。 hello 服務然後取得 hello 最新的金鑰，加密 hello 金鑰，並傳送嗨加密金鑰 toohello 的裝置。

#### <a name="toosynchronize-keys-for-storage-account-credentials-in-hello-same-subscription-as-hello-service-azure-only"></a>中的儲存體帳戶認證的 toosynchronize 金鑰 hello hello 服務 (僅限 Azure) 相同訂用帳戶
1. 在 hello 服務登陸刀鋒視窗中，選取您的服務、 按兩下 hello 服務名稱，然後在 hello**組態**區段中，按一下**儲存體帳戶認證**。
2. 在 hello**儲存體帳戶認證**刀鋒視窗中，在 hello 清單中的儲存體帳戶認證，選取 hello 儲存體帳戶認證的 toosynchronize 之索引鍵。
3. 在 hello**屬性**hello 刀鋒視窗選取儲存體帳戶認證，請勿遵循 hello:
   
    1. 按一下 更多，然後按一下同步存取金鑰。
   
    2. 當提示確認，請按一下**同步處理金鑰**toocomplete hello 同步處理。
    
4. 在 hello StorSimple 裝置管理員服務，您會需要 tooupdate hello 金鑰先前已在 hello Microsoft Azure 儲存體服務中變更。 在 hello**同步處理儲存體帳戶金鑰**刀鋒視窗中，如果 hello 主要存取金鑰已變更 （重新產生），按一下 主要伺服器上，然後再按一下**同步處理金鑰**。 如果 hello 次要索引鍵已變更，請按一下**次要**，然後按一下**同步處理金鑰**。
   
    ![同步存取金鑰](./media/storsimple-virtual-array-manage-storage-accounts/ova-sync-acess-key.png)

## <a name="next-steps"></a>後續步驟
* 了解如何太[管理您的 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md)。

