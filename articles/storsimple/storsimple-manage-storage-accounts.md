---
title: "aaaManage StorSimple 儲存體帳戶 |Microsoft 文件"
description: "說明如何使用 StorSimple Manager 設定頁面 tooadd hello、 編輯、 刪除或旋轉 hello 安全性金鑰的儲存體帳戶。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 93207c40-e0eb-489e-8724-59fb94907081
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/29/2016
ms.author: v-sharos
ms.openlocfilehash: 78f408818ee8532dfaac445200048145547c987c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-your-storage-account"></a>使用 hello StorSimple Manager 服務 toomanage 儲存體帳戶
## <a name="overview"></a>概觀
hello**設定**頁面會顯示所有可由 hello StorSimple Manager 服務的 hello 全域服務參數。 這些參數可以是裝置連線 toohello 服務，並包含套用的 tooall hello:

* 儲存體帳戶 
* 頻寬範本 
* 存取控制記錄 

本教學課程說明如何使用 hello**設定**tooadd、 編輯或刪除儲存體帳戶 頁面上，或旋轉 hello 儲存體帳戶的安全性金鑰。

 ![[設定] 頁面](./media/storsimple-manage-storage-accounts/HCS_ConfigureService.png)  

儲存體帳戶包含 hello hello 裝置使用 tooaccess 與您的雲端服務提供者的儲存體帳戶的認證。 Microsoft Azure 儲存體帳戶，這些是認證，例如 hello 帳戶名稱和 hello 主要存取金鑰。 

在 hello**設定**頁面上，建立 hello 計費訂用帳戶的帳戶會包含下列資訊的 hello 以表格格式顯示所有存放裝置：

* **名稱**– hello 指派唯一名稱 toohello 帳戶建立時。
* **啟用 SSL** – 是否 hello 啟用 SSL，所以裝置到雲端的通訊都會透過 hello 安全通道。
* **使用**– hello 使用 hello 儲存體帳戶的磁碟區數目。

hello 最常見的工作相關 toostorage 帳戶對 hello**設定**頁面：

* 新增儲存體帳戶 
* 編輯儲存體帳戶 
* 刪除儲存體帳戶 
* 替換儲存體帳戶的金鑰 

## <a name="types-of-storage-accounts"></a>儲存體帳戶類型
有三種儲存體帳戶類型能與 StorSimple 裝置搭配使用。

* **自動產生的儲存體帳戶**– 第一次建立 hello 服務時，就 hello 名所示，自動產生這種類型的儲存體帳戶。 toolearn 深入了解如何建立這個儲存體帳戶，請參閱[步驟 1： 建立新的服務](storsimple-deployment-walkthrough-u1.md#step-1-create-a-new-service)中[部署在內部部署 StorSimple 裝置](storsimple-deployment-walkthrough.md)。 
* **Hello 服務訂用帳戶中的儲存體帳戶**– 這些是 hello hello 與相關聯的 Azure 儲存體帳戶相同的訂用帳戶 hello 服務。 toolearn 深入了解如何建立儲存體帳戶，請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。 
* **Hello 服務訂用帳戶以外的儲存體帳戶**-這些是與您的服務沒有關聯的 hello Azure 儲存體帳戶，並可能存在於之前 hello 服務已建立。

## <a name="add-a-storage-account"></a>新增儲存體帳戶
您可以新增儲存體帳戶提供唯一的易記名稱和存取認證連結 toohello 儲存體帳戶 （與 hello 指定的雲端服務提供者）。 您也可以啟用您的裝置與 hello 雲端之間的網路通訊的安全通道 hello 安全通訊端層 (SSL) 模式 toocreate hello 選項。

您可以為指定的雲端服務提供者建立多個帳戶。 不過，請注意，建立儲存體帳戶之後，您無法變更 hello 雲端服務提供者。

正在儲存 hello 儲存體帳戶，而 hello 服務會嘗試 toocommunicate 與您的雲端服務提供者。 在這個階段，將會驗證 hello 認證和您所提供的 hello 存取資料。 只有在 hello 驗證成功時，會建立儲存體帳戶。 如果 hello 驗證失敗，將顯示適當的錯誤訊息。

在 Azure 入口網站中建立的 Resource Manager 儲存體帳戶也支援 StorSimple。 hello 時嘗試 toocreate 磁碟區容器，選取範圍的 hello 下拉式清單中將不會顯示儲存體帳戶的資源管理員只 hello hello Azure 傳統入口網站中建立的帳戶將會顯示儲存體。 資源管理員的儲存體帳戶將需要使用 hello 程序 tooadd 如下所述的儲存體帳戶加入 toobe。

> [!NOTE]
> 新增儲存體帳戶的 hello 程序不同根據您所使用的 hello StorSimple 軟體版本。 為確定 toofollow hello 正確的程序適用於您的 StorSimple 版本。
> 
> 

[!INCLUDE [add-a-storage-account-update1](../../includes/storsimple-configure-new-storage-account-u1.md)]

[!INCLUDE [add-a-storage-account](../../includes/storsimple-configure-new-storage-account.md)]

## <a name="edit-a-storage-account"></a>編輯儲存體帳戶
您可以編輯磁碟區容器所使用的儲存體帳戶。 如果您編輯目前正在使用的儲存體帳戶，hello 欄位可用 toomodify 是 hello hello 儲存體帳戶的存取金鑰。 您可以提供 hello 新儲存體存取金鑰，並儲存更新的 hello 設定。

#### <a name="tooedit-a-storage-account"></a>tooedit 儲存體帳戶
1. 在 hello 服務登陸頁面上，選取您的服務、 按兩下 hello 的服務名稱，然後按一下**設定**。
2. 按一下 [新增/編輯儲存體帳戶] 。
3. 在 hello**新增/編輯儲存體帳戶**對話方塊：
   
   1. Hello 下拉式清單中**儲存體帳戶**，選擇您想要 toomodify 現有的帳戶。 這也可能包括 hello hello 服務第一次建立時自動產生的儲存體帳戶。
   2. 如果有必要，您可以修改 hello**啟用 SSL 模式**選取項目。
   3. 您可以選擇 toorotate 儲存體帳戶存取金鑰。 請參閱[金鑰輪替的儲存體帳戶](#key-rotation-of-storage-accounts)如需有關如何 tooperform 金鑰輪替。
   4. 按一下核取圖示，hello![核取圖示](./media/storsimple-manage-storage-accounts/HCS_CheckIcon.png)toosave hello 設定。 hello 設定將更新上 hello**設定**頁面。 按一下**儲存**toosave hello 新更新的設定。
      
      ![編輯儲存體帳戶](./media/storsimple-manage-storage-accounts/HCs_AddEditStorageAccount.png)

## <a name="delete-a-storage-account"></a>刪除儲存體帳戶
> [!IMPORTANT]
> 只有在其未由磁碟區容器使用時，您才可以刪除儲存體帳戶。 如果磁碟區容器正在使用的儲存體帳戶，請先刪除 hello 磁碟區容器，然後再刪除相關聯的 hello 儲存體帳戶。
> 
> 

#### <a name="toodelete-a-storage-account"></a>toodelete 儲存體帳戶
1. 在 hello StorSimple Manager 服務登陸頁面上，選取您的服務、 按兩下 hello 的服務名稱，然後按一下**設定**。
2. 在 hello 表格式清單中的儲存體帳戶，請將滑鼠停留在您想 toodelete hello 帳戶。
3. 刪除圖示 (**x**) 會出現在 hello 極端右側的欄該儲存體帳戶。 按一下 hello **x**圖示 toodelete hello 認證。
4. 當提示確認，請按一下**是**toocontinue 與 hello 刪除。 hello 表格式清單將會更新的 tooreflect hello 的變更。

## <a name="key-rotation-of-storage-accounts"></a>替換儲存體帳戶的金鑰
基於安全性理由，通常是在資料中心內才需要替換金鑰。 

> [!NOTE]
> hello 更換金鑰資訊與 hello 旋轉的程序適用於僅 tooMicrosoft Azure 儲存體帳戶。 若您使用的是其他雲端服務提供者，可以透過該提供者的儀表板管理儲存體帳戶金鑰。
> 
> 

每個 Microsoft Azure 訂用帳戶可以有一或多個相關聯的儲存體帳戶。 hello 存取 toothese 帳戶受到 hello 訂用帳戶和每個儲存體帳戶存取金鑰。 

當您建立儲存體帳戶時，Microsoft Azure 會產生兩個存取 hello 儲存體帳戶時，可用於驗證的 512 位元儲存體存取金鑰。 必須要有兩個儲存體存取金鑰可讓您使用不中斷 tooyour 儲存體服務或存取 toothat 服務 tooregenerate hello 索引鍵。 hello 目前正在使用的索引鍵為 hello*主要*索引鍵和 hello 備份金鑰是參照的 tooas hello*次要*索引鍵。 當 Microsoft Azure StorSimple 裝置存取您的雲端儲存體服務提供者時必須提供這些兩個機碼之一。

## <a name="what-is-key-rotation"></a>什麼是替換金鑰？
一般而言，應用程式使用其中一個 hello 金鑰 tooaccess 您的資料。 在一段時間之後, 您可以讓應用程式切換 toousing hello 第二個索引鍵。 切換應用程式 toohello 的次要金鑰之後，您可以淘汰 hello 第一個索引鍵，並再產生新的金鑰。 使用 hello 兩個索引鍵，如此一來，可以讓應用程式存取 toohello 資料而不會產生任何停機時間。

hello 儲存體帳戶金鑰一律儲存在 hello 服務，以加密格式。 不過，這些可以重設透過 hello StorSimple Manager 服務。 hello 服務可以取得 hello 主索引鍵和次要索引鍵的所有 hello 的 hello 相同訂用帳戶，包括 hello 儲存體服務，以及 hello 預設儲存體帳戶中建立的帳戶產生的儲存體帳戶時 hello StorSimple Manager 服務第一次建立服務。 hello StorSimple Manager 服務將一律從 hello Azure 傳統入口網站取得這些金鑰，然後以加密方式儲存。

## <a name="rotation-workflow"></a>替換工作流程
Microsoft Azure 系統管理員可以重新產生，或藉由直接存取 hello （透過 hello Microsoft Azure 儲存體服務) 的儲存體帳戶變更 hello 主要或次要金鑰。 hello StorSimple Manager 服務不會自動看到這項變更。

tooinform hello StorSimple Manager 服務的 hello 變更，您將需要 tooaccess hello StorSimple Manager 服務存取 hello 儲存體帳戶，然後再同步處理 hello 主要或次要金鑰 （視何者有所變更）。 hello 服務然後取得 hello 最新的金鑰，加密 hello 金鑰，並傳送嗨加密金鑰 toohello 的裝置。

#### <a name="toosynchronize-keys-for-storage-accounts-in-hello-same-subscription-as-hello-service-azure-only"></a>儲存體帳戶的 toosynchronize 金鑰 hello hello 服務 (僅限 Azure) 相同訂用帳戶
1. 在 [hello**服務**頁面上，按一下 hello**設定**] 索引標籤。
2. 按一下 [新增/編輯儲存體帳戶] 。
3. 在 [hello] 對話方塊中，請勿 hello 遵循：
   
   1. 選取 hello 儲存體帳戶與 hello 索引鍵的 toosynchronize。 在顯示時，會加密 hello 儲存體帳戶金鑰。
   2. 在 hello StorSimple Manager 服務，您會需要 tooupdate hello 金鑰先前已在 hello Microsoft Azure 儲存體服務中變更。 如果 hello 主要存取金鑰已變更 （重新產生），按一下**同步處理主要金鑰**。 如果 hello 次要索引鍵已變更，請按一下**同步處理次要金鑰**。
      
      ![同步處理金鑰](./media/storsimple-manage-storage-accounts/HCS_KeyRotationStorageAccountSameSubscriptionAsService.png)

#### <a name="toosynchronize-keys-for-storage-accounts-outside-of-hello-service-subscription"></a>toosynchronize hello 服務訂用帳戶以外的儲存體帳戶金鑰
1. 在 [hello**服務**頁面上，按一下 hello**設定**] 索引標籤。
2. 按一下 [新增/編輯儲存體帳戶] 。
3. 在 [hello] 對話方塊中，請勿 hello 遵循：
   
   1. 選取 hello 儲存體帳戶與 hello 便捷鍵的 tooupdate。
   2. 您必須在 StorSimple Manager 服務的 hello tooupdate hello 儲存體存取金鑰。 在此情況下，您可以看到 hello 儲存體存取金鑰。 輸入 hello 新金鑰在 hello**儲存體帳戶存取金鑰**y 方塊。 
   3. 儲存您的變更。 現在應已更新您的儲存體帳戶存取金鑰。

## <a name="next-steps"></a>後續步驟
* 深入了解 [StorSimple 安全性](storsimple-security.md)。
* 深入了解[使用您的 StorSimple 裝置 hello StorSimple Manager 服務 tooadminister](storsimple-manager-service-administration.md)。

