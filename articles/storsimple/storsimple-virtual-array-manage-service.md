---
title: "aaaDeploy StorSimple 裝置管理員服務 |Microsoft 文件"
description: "說明如何 toocreate 和 delete hello hello Azure 入口網站中的 StorSimple 裝置管理員服務以及 toomanage hello 服務登錄機碼的方式。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 28499494-8c4d-4a7f-9d44-94b2b8a93c93
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: alkohli
ms.openlocfilehash: 9064053addc7b3dfcce08b47e81b38c2e0e1b559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-virtual-array"></a>部署 StorSimple Virtual Array 的 hello StorSimple 裝置管理員服務
## <a name="overview"></a>概觀

hello StorSimple 裝置管理員服務在 Microsoft Azure 中執行，並連接 toomultiple StorSimple 裝置。 建立 hello 服務之後，您可以使用它 toomanage hello 裝置 hello Microsoft Azure 入口網站瀏覽器中執行。 這可讓您 toomonitor 所有 hello 的裝置連線的 toohello StorSimple 裝置管理員都服務從單一中央位置，藉此將管理負擔降至最低。

hello 常見工作相關的 tooa StorSimple 裝置管理員服務如下：

* 建立服務
* 刪除服務
* 取得 hello 服務註冊金鑰
* 重新產生 hello 服務註冊金鑰

本教學課程說明如何 tooperform 每個的 hello 前面的工作。 這篇文章中所包含的 hello 資訊是適用於只有 tooStorSimple 虛擬的陣列。 如需 StorSimple 8000 系列的詳細資訊，請移至太[部署 StorSimple Manager 服務](storsimple-manage-service.md)。

## <a name="create-a-service"></a>建立服務

toocreate 服務，您需要 toohave:

* 具有企業合約的訂用帳戶
* 使用中的 Microsoft Azure 儲存體帳戶
* hello 用於存取管理的計費資訊

您也可以選擇 toogenerate 儲存體帳戶建立 hello 服務時。

單一服務可以管理多個裝置。 不過，裝置不能跨越多個服務。 大型企業可以擁有多個服務執行個體 toowork 與不同的訂閱、 組織或甚至是部署位置。

> [!NOTE]
> 您需要不同的 StorSimple 裝置管理員服務 toomanage StorSimple 8000 系列裝置和 StorSimple 虛擬陣列執行個體。


執行下列步驟 toocreate 服務的 hello。

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a>刪除服務

刪除服務之前，請確定沒有任何連接的裝置正在使用它。 如果 hello 服務正在使用中，停用 hello 連接裝置。 hello 停用作業將會斷絕 hello hello 裝置與 hello 服務之間的連接，但是會保留 hello 雲端中的 hello 裝置資料。

> [!IMPORTANT]
> 刪除服務之後，hello 作業無法反轉。 已使用 hello 服務的任何裝置需要 toobe 原廠重設之前可以搭配另一個服務。 在此案例中，hello hello 裝置，以及 hello 組態上的本機資料將會遺失。
 

執行下列步驟 toodelete 服務的 hello。

#### <a name="toodelete-a-service"></a>toodelete 服務

1. 跳過**所有資源**。 搜尋您的 StorSimple 裝置管理員服務。 選取您想 toodelete hello 服務。
   
    ![選取服務 toodelete](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. 移 tooyour 服務儀表板 tooensure 有無任何裝置已連線 toohello 服務。 如果沒有與此服務註冊的裝置，也會看到橫幅訊息 toohello 效果。 按一下 [刪除] 。
   
    ![刪除服務](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. 當提示確認，請按一下**是**hello 確認通知中。 
   
    ![確認刪除服務](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. 可能需要幾分鐘，讓 hello 服務 toobe 刪除。 Hello 服務已成功刪除之後，系統會通知您。
   
    ![成功刪除服務](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

服務的 hello 清單會重新整理。

 ![更新的服務清單](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-hello-service-registration-key"></a>取得 hello 服務註冊金鑰
您已成功建立服務之後，您將需要 tooregister hello 服務您 StorSimple 裝置。 tooregister 第一個 StorSimple 裝置，您將需要 hello 服務註冊金鑰。 tooregister 現有 StorSimple 服務的其他裝置，您將需要 hello 註冊金鑰和 hello 服務資料加密金鑰 （這在註冊期間產生 hello 第一個裝置上）。 如需 hello 服務資料加密金鑰的詳細資訊，請參閱[StorSimple 安全性](storsimple-security.md)。 您可以藉由存取 hello 取得 hello 登錄機碼**金鑰**刀鋒視窗中為您的服務。

執行下列步驟 tooget hello 服務登錄機碼的 hello。

#### <a name="tooget-hello-service-registration-key"></a>tooget hello 服務註冊金鑰
1. 在 hello **StorSimple 裝置管理員**刀鋒視窗中，跳過**管理&gt;**  **金鑰**。
   
   ![[金鑰] 刀鋒視窗](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. 在 hello**金鑰**刀鋒視窗中，會出現服務註冊金鑰。 複製使用 hello 複製圖示 hello 註冊金鑰。 

將 hello 服務註冊金鑰保存在安全的位置。 您將需要此金鑰，以及 hello 服務資料加密金鑰，tooregister 其他裝置向此服務。 取得之後 hello 服務註冊金鑰，您需要 tooconfigure 您的裝置 hello Windows PowerShell 透過 StorSimple 介面。

## <a name="regenerate-hello-service-registration-key"></a>重新產生 hello 服務註冊金鑰
如果您被需要的 tooperform 金鑰輪動或服務管理員 hello 清單是否已變更，您將需要 tooregenerate 服務註冊金鑰。 當您重新產生 hello 索引鍵時，hello 新的金鑰僅用於註冊後續的裝置。 hello 已經註冊的裝置不會影響此處理程序。

執行下列步驟 tooregenerate 服務註冊金鑰的 hello。

#### <a name="tooregenerate-hello-service-registration-key"></a>tooregenerate hello 服務註冊金鑰
1. 在 hello **StorSimple 裝置管理員**刀鋒視窗中，跳過**管理&gt;**  **金鑰**。
   
   ![[金鑰] 刀鋒視窗](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. 在 hello**金鑰**刀鋒視窗中，按一下 **重新產生**。
   
   ![按一下重新產生](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. 在 hello**重新產生服務登錄機碼**刀鋒視窗中，檢閱 hello 動作時才需要 hello 重新產生金鑰。 所有 hello 後續裝置註冊的此服務會都使用 hello 新的註冊金鑰。 按一下**重新產生**tooconfirm。 Hello 註冊完成後，系統會通知您。
   
   ![確認重新產生金鑰](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. 新的服務註冊金鑰隨即顯示。
   
    ![確認重新產生金鑰](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   複製這個金鑰並儲存，以對任何新的裝置註冊此服務。

## <a name="next-steps"></a>後續步驟
* 了解如何太[開始](storsimple-virtual-array-deploy1-portal-prep.md)與 StorSimple Virtual Array。
* 了解如何太[管理您的 StorSimple 裝置](storsimple-ova-web-ui-admin.md)。

