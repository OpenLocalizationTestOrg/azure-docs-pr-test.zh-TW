---
title: "aaaDeploy hello StorSimple Manager 服務 |Microsoft 文件"
description: "說明 toocreate 和 delete hello StorSimple Manager 服務在 hello Azure 傳統入口網站，以及如何 toomanage hello 服務註冊金鑰。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: bc1d5650-275c-42ed-bc77-cdb596f85943
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f49b647d91b03bb89ebd0e5cce196e50e3c00296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-manager-service-in-hello-azure-classic-portal"></a>部署在 hello Azure 傳統入口網站中的 hello StorSimple Manager 服務

## <a name="overview"></a>概觀
hello StorSimple Manager 服務在 Microsoft Azure 中執行，並連接 toomultiple StorSimple 裝置。 建立 hello 服務之後，您可以使用它 toomanage hello 裝置 hello Microsoft Azure 傳統入口網站瀏覽器中執行。 這可讓您 toomonitor 所有 hello 的裝置連線的 toohello StorSimple Manager 都服務從單一中央位置，藉此將管理負擔降至最低。

hello StorSimple Manager 登陸頁面列出所有 hello StorSimple Manager 服務，您可以使用 toomanage StorSimple 儲存體裝置。 每個 StorSimple Manager 服務，hello 下列資訊是針對顯示 hello StorSimple 管理員 頁面上：

* **名稱**– 建立時指派 tooyour StorSimple Manager 服務的 hello 名稱。 **建立 hello 服務之後，就無法變更 hello 服務名稱。這也適用於其他實體，例如裝置、 磁碟區、 磁碟區容器和備份原則不能在 hello Azure 傳統入口網站中重新命名。**
* **狀態**– hello hello 服務狀態，它可以是**Active**，**建立**，或**線上**。
* **位置**– hello 地理位置中的 hello StorSimple 裝置將會部署。
* **訂用帳戶**– hello 帳單與服務相關聯的訂用帳戶。

hello 可透過 hello StorSimple Manager 頁面執行的一般工作包括：

* 建立服務
* 刪除服務
* 取得 hello 服務註冊金鑰
* 重新產生 hello 服務註冊金鑰

這個教學課程描述如何 tooperform 每個這些工作。

## <a name="create-a-service"></a>建立服務
使用 hello**快速建立**選項 toocreate StorSimple Manager 服務，如果您想 toodeploy StorSimple 裝置。 toocreate 服務，您需要 toohave:

* 具有企業合約的訂用帳戶
* 使用中的 Microsoft Azure 儲存體帳戶
* hello 用於存取管理的計費資訊

您也可以選擇 toogenerate 預設儲存體帳戶建立 hello 服務時。

單一服務可以管理多個裝置。 不過，裝置不能跨越多個服務。 大型企業可以擁有多個服務執行個體 toowork 與不同的訂閱、 組織或甚至是部署位置。 請注意，您需要不同的 StorSimple Manager 服務 toomanage StorSimple 8000 系列裝置和 StorSimple 虛擬陣列的執行個體。

> [!IMPORTANT] 
> 如果您有建立未使用的服務 （沒有這項資源執行作業的裝置） 先前 tooAugust 2016，它無法透過 Azure 入口網站或 Azure 傳統入口網站進行管理。 我們建議您在 hello Azure 入口網站中建立新的服務。

執行下列步驟 toocreate 服務的 hello。

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

## <a name="delete-a-service"></a>刪除服務
刪除服務之前，請確定沒有任何連接的裝置正在使用它。 如果 hello 服務正在使用中，停用 hello 連接裝置。 hello 停用作業將會斷絕 hello hello 裝置與 hello 服務之間的連接，但是會保留 hello 雲端中的 hello 裝置資料。

> [!IMPORTANT] 
> 刪除服務之後，hello 作業無法反轉。 已使用 hello 服務的任何裝置需要 toobe 原廠重設之前可以搭配另一個服務。 在此案例中，hello hello 裝置，以及 hello 組態上的本機資料將會遺失。

執行下列步驟 toodelete 服務的 hello。

### <a name="toodelete-a-service"></a>toodelete 服務
1. 在 hello **StorSimple Manager 服務**頁面上，且想 toodelete 選取 hello 服務。
2. 按一下**刪除**hello hello 頁底端。
3. 按一下**是**hello 確認通知中。 可能需要幾分鐘，讓 hello 服務 toobe 刪除。

## <a name="get-hello-service-registration-key"></a>取得 hello 服務註冊金鑰
您已成功建立服務之後，您將需要 tooregister hello 服務您 StorSimple 裝置。 tooregister 第一個 StorSimple 裝置，您將需要 hello 服務註冊金鑰。 tooregister 現有 StorSimple 服務的其他裝置，您將需要 hello 註冊金鑰和 hello 服務資料加密金鑰 （這在註冊期間產生 hello 第一個裝置上）。 如需 hello 服務資料加密金鑰的詳細資訊，請參閱[StorSimple 安全性](storsimple-security.md)。 您可以存取，以取得 hello 登錄機碼**登錄機碼**上 hello**服務**頁面。

執行下列步驟 tooget hello 服務登錄機碼的 hello。

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

將 hello 服務註冊金鑰保存在安全的位置。 您將需要此金鑰，以及 hello 服務資料加密金鑰，tooregister 其他裝置向此服務。 取得之後 hello 服務註冊金鑰，您需要 tooconfigure 您的裝置 hello Windows PowerShell 透過 StorSimple 介面。

如需詳細資訊，如何 toouse 這個註冊金鑰，請參閱[步驟 3： 設定和註冊 hello 裝置透過 Windows PowerShell for StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)。

## <a name="regenerate-hello-service-registration-key"></a>重新產生 hello 服務註冊金鑰
如果您被需要的 tooperform 金鑰輪動或服務管理員 hello 清單是否已變更，您將需要 tooregenerate 服務註冊金鑰。 當您重新產生 hello 索引鍵時，hello 新的金鑰僅用於註冊後續的裝置。 hello 已經註冊的裝置不會影響此處理程序。

執行下列步驟 tooregenerate 服務註冊金鑰的 hello。

### <a name="tooregenerate-hello-service-registration-key"></a>tooregenerate hello 服務註冊金鑰
1. 在 hello **StorSimple Manager 服務**頁面上，按一下**登錄機碼**。
2. 在 hello**服務註冊金鑰**對話方塊中，按一下 **重新產生**。
3. 您將會看見確認訊息。 按一下**確定**toocontinue 與 hello 重新產生。
4. 新的服務註冊金鑰隨即顯示。
5. 複製這個金鑰並儲存，以對任何新的裝置註冊此服務。
6. 按一下 [hello] 核取圖示 ![核取圖示](./media/storsimple-manage-service/HCS_CheckIcon.png) tooclose 此對話方塊。

## <a name="next-steps"></a>後續步驟
* 深入了解 hello [StorSimple 部署程序](storsimple-deployment-walkthrough-u2.md)。
* 深入了解 [管理 StorSimple 儲存體帳戶](storsimple-manage-storage-accounts.md)。
* 深入了解如何太[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。
