---
title: "aaaDeploy hello Azure StorSimple 裝置管理員服務 |Microsoft 文件"
description: "說明如何 toocreate 和 delete hello hello Azure 入口網站中的 StorSimple 裝置管理員服務以及 toomanage hello 服務登錄機碼的方式。"
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
ms.date: 07/13/2017
ms.author: alkohli
ms.openlocfilehash: b84a907d6b735c8fee7bdc51f9c0074857297d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-8000-series-devices"></a>部署適用於 StorSimple 8000 系列裝置 hello StorSimple 裝置管理員服務

## <a name="overview"></a>概觀

hello StorSimple 裝置管理員服務在 Microsoft Azure 中執行，並連接 toomultiple StorSimple 裝置。 建立 hello 服務之後，您可以使用它 toomanage 所有 hello 的裝置連線的 toohello StorSimple 裝置管理員都服務從單一中央位置，藉此將管理負擔降至最低。

本教學課程描述 hello hello 建立、 刪除、 hello 服務移轉與 hello hello 服務登錄機碼管理所需的步驟。 這篇文章中所包含的 hello 資訊是適用於只有 tooStorSimple 8000 系列的裝置。 如需 StorSimple 虛擬陣列的詳細資訊，請移至太[部署 StorSimple 裝置管理員服務為您的 StorSimple Virtual Array](storsimple-virtual-array-manage-service.md)。

## <a name="create-a-service"></a>建立服務
toocreate StorSimple 裝置管理員服務，您需要 toohave:

* 具有企業合約的訂用帳戶
* 使用中的 Microsoft Azure 儲存體帳戶
* hello 用於存取管理的計費資訊

允許只 hello 與 Enterprise 合約的訂閱。 Hello Azure 入口網站中不支援 Microsoft 發起者訂閱 hello Azure 傳統入口網站中所允許的。 您會看到下列訊息時使用不支援的訂閱 hello:

![訂用帳戶無效](./media/storsimple-8000-manage-service/subscription-not-valid.jpg)

您也可以選擇 toogenerate 預設儲存體帳戶建立 hello 服務時。

單一服務可以管理多個裝置。 不過，裝置不能跨越多個服務。 大型企業可以擁有多個服務執行個體 toowork 與不同的訂閱、 組織或甚至是部署位置。 

> [!NOTE]
> 您需要不同的 StorSimple 裝置管理員服務 toomanage StorSimple 8000 系列裝置和 StorSimple 虛擬陣列執行個體。

執行下列步驟 toocreate 服務的 hello。

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-8000-create-new-service.md)]


每個 StorSimple 裝置管理員服務，下列屬性的 hello 存在：

* **名稱**– 建立時指派 tooyour StorSimple 裝置管理員服務的 hello 名稱。 **建立 hello 服務之後，就無法變更 hello 服務名稱。這也適用於其他實體，例如裝置、 磁碟區、 磁碟區容器和備份原則不能在 hello Azure 入口網站中重新命名。**
* **狀態**– hello hello 服務狀態，它可以是**Active**，**建立**，或**線上**。
* **位置**– hello 地理位置中的 hello StorSimple 裝置將會部署。
* **訂用帳戶**– hello 帳單與服務相關聯的訂用帳戶。

## <a name="move-a-service-tooazure-portal"></a>將服務 tooAzure 入口網站移
StorSimple 8000 系列可以立即管理 hello Azure 入口網站中。 如果您有現有服務 toomanage hello StorSimple 裝置時，我們建議您移動您服務 toohello Azure 入口網站。 2017 年 9 月 30 後, 就無法使用 hello hello StorSimple Manager 服務的 Azure 傳統入口網站。

使用分階段 hello 選項 toomigrate toohello Azure 入口網站。 如果您沒有看到選項 toomigrate tooAzure 入口網站，但是您想 toomove 並檢閱移轉的 hello 影響述 hello[考量轉換](#considerations-for-transition)，您可以[提交要求](https://aka.ms/ss8000-cx-signup)。

### <a name="considerations-for-transition"></a>轉換之前

在您移動 hello 服務之前，請檢閱 hello 影響移轉 toohello 新版的 Azure 入口網站。

#### <a name="before-you-transition"></a>轉換前的注意事項

* 裝置需執行 Update 3.0 或更新版本。 如果您的裝置正在執行較舊的版本，安裝 hello 最新的更新。 如需詳細資訊，請移至太[安裝 Update 4](storsimple-8000-install-update-4.md)。 如果使用 StorSimple 雲端設備 (8010/8020)，請以 Update 4.0 建立新的雲端設備。 

* 一旦轉換的 toohello 新版 Azure 入口網站，您無法使用 Azure 傳統入口網站 toomanage hello StorSimple 裝置。

* hello 轉換非干擾性，而且沒有 hello 裝置不再停機時間。

* 所有在 hello hello StorSimple 裝置管理員指定的訂用帳戶會轉換。

#### <a name="during-hello-transition"></a>Hello 轉換期間

* 您無法從 hello 入口網站來管理您的裝置。
* 例如階層處理和已排程備份的作業繼續進行 toooccur。
* 請勿刪除 hello 轉換正在進行時 hello 舊的 StorSimple 裝置管理員。

#### <a name="after-hello-transition"></a>Hello 轉換之後

* 您無法再從 hello 傳統入口網站管理您的裝置。

* 不支援 hello 現有的 Azure 服務管理 (ASM) PowerShell cmdlet。 更新 hello 指令碼 toomanage hello Azure 資源管理員透過您的裝置。

* 您的服務和裝置設定會予以保留。 所有磁碟區和備份也是轉換的 toohello Azure 入口網站。

### <a name="begin-transition"></a>開始轉換

執行下列步驟 tootransition hello 您服務 toohello Azure 入口網站。

1. 移 hello 傳統入口網站中的 tooyour 現有 StorSimple Manager 服務。

2. 您看到通知，通知您 hello StorSimple 裝置管理員服務現已推出 hello Azure 入口網站。 請注意在 hello Azure 入口網站，hello 服務會參照的 tooas StorSimple 裝置管理員服務。

    ![移轉通知](./media/storsimple-8000-manage-service/service-transition1.jpg)

    1. 請確定您已檢閱 hello 移轉的完整影響。
    2. 檢閱 hello 清單將從 hello 傳統入口網站移的 StorSimple 裝置管理員。

3. 按一下 [移轉]。 hello 轉換開始，並採用幾分鐘的時間 toocomplete。

Hello 轉換完成之後，您可以管理您的裝置透過 hello hello Azure 入口網站中的 StorSimple 裝置管理員服務。

在 hello Azure 入口網站，只 hello 執行 Update 3.0 的 StorSimple 裝置，支援更高版本。 執行較舊版本的 hello 裝置的支援有限。 hello 下列資料表 summrizes hello 裝置執行 versios 先前 tooUpdate 3.0 中，一旦移轉自 hello 傳統 toohello Azure 入口網站支援的作業。

| 作業                                                                                                                       | 支援      |
|---------------------------------------------------------------------------------------------------------------------------------|----------------|
| 註冊裝置                                                                                                               | 是            |
| 設定裝置設定，例如一般設定、網路設定和安全性設定                                                                | 是            |
| 掃描、下載，及安裝更新                                                                                             | 是            |
| 停用裝置                                                                                                               | 是            |
| 刪除裝置                                                                                                                   | 是            |
| 建立、修改及刪除磁碟區容器                                                                                   | 否             |
| 建立、修改及刪除磁碟區                                                                                             | 否             |
| 建立、修改及刪除備份原則                                                                                      | 否             |
| 進行手動備份                                                                                                            | 否             |
| 進行排程備份                                                                                                         | 不適用 |
| 從備份組還原                                                                                                        | 否             |
| 3.0 和更新版本執行更新的複製品 tooa 裝置 <br> hello 來源裝置正在執行版本先前 tooUpdate 3.0。                                | 是            |
| 執行版本先前 tooUpdate 3.0 複製 tooa 裝置                                                                          | 否             |
| 作為容錯移轉的來源裝置 <br> （從執行 3.0 和更新版本，執行更新的版本先前 tooUpdate 3.0 tooa 裝置的裝置）                                                               | 是            |
| 作為容錯移轉的目標裝置 <br> （tooa 裝置執行軟體版本先前 tooUpdate 3.0）                                                                                   | 否             |
| 清除警示                                                                                                                  | 是            |
| 檢視備份原則、備份類別目錄、磁碟區、磁碟區容器、監視圖表、作業，以及傳統入口網站中建立的警示 | 是            |
| 開啟和關閉裝置控制器                                                                                              | 是            |


## <a name="delete-a-service"></a>刪除服務

刪除服務之前，請確定沒有任何連接的裝置正在使用它。 如果 hello 服務正在使用中，停用 hello 連接裝置。 hello 停用作業將會斷絕 hello hello 裝置與 hello 服務之間的連接，但是會保留 hello 雲端中的 hello 裝置資料。

> [!IMPORTANT]
> 刪除服務之後，hello 作業無法反轉。 已使用 hello 服務的任何裝置需要 toobe 重設 toofactory 預設值，然後搭配另一個服務。 在此案例中，hello hello 裝置，以及 hello 組態上的本機資料將會遺失。

執行下列步驟 toodelete 服務的 hello。

### <a name="toodelete-a-service"></a>toodelete 服務

1. 搜尋您想 toodelete hello 服務。 按一下**資源**圖示，然後輸入 hello 適當條款 toosearch。 在 hello 搜尋結果中，按一下您想要 toodelete hello 服務。

    ![搜尋服務 toodelete](./media/storsimple-8000-manage-service/deletessdevman1.png)

2. 這會帶您 toohello StorSimple 裝置管理員服務刀鋒視窗。 按一下 [刪除] 。

    ![刪除服務](./media/storsimple-8000-manage-service/deletessdevman2.png)

3. 按一下**是**hello 確認通知中。 可能需要幾分鐘，讓 hello 服務 toobe 刪除。

    ![確認刪除](./media/storsimple-8000-manage-service/deletessdevman3.png)

## <a name="get-hello-service-registration-key"></a>取得 hello 服務註冊金鑰

您已成功建立服務之後，您將需要 tooregister hello 服務您 StorSimple 裝置。 tooregister 第一個 StorSimple 裝置，您將需要 hello 服務註冊金鑰。 tooregister 現有 StorSimple 服務的其他裝置，您需要 hello 註冊金鑰和 hello 服務資料加密金鑰 （這在註冊期間產生 hello 第一個裝置上）。 如需 hello 服務資料加密金鑰的詳細資訊，請參閱[StorSimple 安全性](storsimple-8000-security.md)。 您可以存取，以取得 hello 登錄機碼**金鑰**您 StorSimple 裝置管理員 刀鋒視窗。

執行下列步驟 tooget hello 服務登錄機碼的 hello。

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

將 hello 服務註冊金鑰保存在安全的位置。 您將需要此金鑰，以及 hello 服務資料加密金鑰，tooregister 其他裝置向此服務。 取得之後 hello 服務註冊金鑰，您必須設定您的裝置 hello Windows PowerShell 透過 StorSimple 介面。

如需詳細資訊，如何 toouse 這個註冊金鑰，請參閱[步驟 3： 設定和註冊 hello 裝置透過 Windows PowerShell for StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)。

## <a name="regenerate-hello-service-registration-key"></a>重新產生 hello 服務註冊金鑰
如果您被需要的 tooperform 金鑰輪動或服務管理員 hello 清單是否已變更，您會需要 tooregenerate 服務註冊金鑰。 當您重新產生 hello 索引鍵時，hello 新的金鑰僅用於註冊後續的裝置。 hello 已經註冊的裝置不會影響此處理程序。

執行下列步驟 tooregenerate 服務註冊金鑰的 hello。

### <a name="tooregenerate-hello-service-registration-key"></a>tooregenerate hello 服務註冊金鑰
1. 在 hello **StorSimple 裝置管理員**刀鋒視窗中，跳過**管理&gt;**  **金鑰**。
    
    ![[金鑰] 刀鋒視窗](./media/storsimple-8000-manage-service/regenregkey2.png)

2. 在 hello**金鑰**刀鋒視窗中，按一下 **重新產生**。

    ![按一下重新產生](./media/storsimple-8000-manage-service/regenregkey3.png)
3. 在 hello**重新產生服務登錄機碼**刀鋒視窗中，檢閱 hello 動作時才需要 hello 重新產生金鑰。 所有 hello 後續裝置註冊的此服務會都使用 hello 新的註冊金鑰。 按一下**重新產生**tooconfirm。 Hello 重新產生作業完成之後，您會收到通知。

    ![確認重新產生](./media/storsimple-8000-manage-service/regenregkey4.png)

4. 新的服務註冊金鑰隨即顯示。

5. 複製這個金鑰並儲存，以對任何新的裝置註冊此服務。



## <a name="change-hello-service-data-encryption-key"></a>變更 hello 服務資料加密金鑰
服務資料加密金鑰是使用的 tooencrypt 客戶機密資料，例如從 StorSimple Manager 服務 toohello StorSimple 裝置傳送的儲存體帳戶認證。 您將需要 toochange 這些機碼定期如果您的 IT 組織具有 hello 存放裝置金鑰輪動原則。 hello 金鑰變更程序可能會稍有不同，視沒有單一裝置或多個 hello StorSimple Manager 服務所管理的裝置。 如需詳細資訊，請移至太[StorSimple 安全性和資料保護](storsimple-8000-security.md)。

變更 hello 服務資料加密金鑰是 3 個步驟程序：

1. 使用 Windows PowerShell 指令碼的 Azure 資源管理員，授權裝置 toochange hello 服務資料加密金鑰。
2. 使用 Windows PowerShell for StorSimple，起始 hello 服務資料加密金鑰變更。
3. 如果您有多個 StorSimple 裝置，更新其他裝置上 hello hello 服務資料加密金鑰。

### <a name="step-1-use-windows-powershell-script-tooauthorize-a-device-toochange-hello-service-data-encryption-key"></a>步驟 1： 使用 Windows PowerShell 指令碼 tooAuthorize 裝置 toochange hello 服務資料加密金鑰
一般而言，hello 裝置系統管理員會要求該 hello 服務系統管理員授權裝置 toochange 服務資料加密金鑰。 然後 hello 服務系統管理員將授權 hello 裝置 toochange hello 機碼。

使用 hello 基礎的 Azure 資源管理員指令碼來執行此步驟。 hello 服務系統管理員可以選取適合 toobe 獲授權的裝置。 hello 裝置處於已授權的 toostart hello 服務資料加密金鑰變更程序。 

如需有關使用 hello 指令碼的詳細資訊，請移至太[授權 ServiceEncryptionRollover.ps1](https://github.com/anoobbacker/storsimpledevicemgmttools/blob/master/Authorize-ServiceEncryptionRollover.ps1)

#### <a name="which-devices-can-be-authorized-toochange-service-data-encryption-keys"></a>哪些裝置可以被授權 toochange 服務資料加密金鑰？
裝置必須符合下列準則，它可以是授權的 tooinitiate 服務資料加密金鑰變更之前的 hello:

* hello 裝置必須是線上 toobe 適合服務資料加密金鑰變更授權。
* 您可以授權的 hello 相同裝置一次在 30 分鐘後如果 hello 金鑰變更未起始。
* 您可以授權另一個裝置，前提 hello 金鑰變更未起始 hello 先前授權的裝置。 已獲授權 hello 新裝置之後，hello 舊裝置無法起始 hello 變更。
* Hello hello 服務資料加密金鑰變換正在進行時，您無法授權裝置。
* 某些 hello hello 服務中註冊的裝置已變換 hello 加密而其他裝置尚未時，您可以授權裝置。 

### <a name="step-2-use-windows-powershell-for-storsimple-tooinitiate-hello-service-data-encryption-key-change"></a>步驟 2： 使用 Windows PowerShell for StorSimple tooinitiate hello 服務資料加密金鑰變更
StorSimple 介面上 hello 授權 StorSimple 裝置的 hello Windows PowerShell 會執行此步驟。

> [!NOTE]
> Hello 金鑰變換完成之前，可以在 hello 的 StorSimple Manager 服務的 Azure 入口網站中不執行任何作業。
> 
> 

如果您使用 hello 裝置序列主控台 tooconnect toohello Windows PowerShell 介面，執行下列步驟的 hello。

#### <a name="tooinitiate-hello-service-data-encryption-key-change"></a>tooinitiate hello 服務資料加密金鑰變更
1. 選取選項 1 toolog 上，具有完整存取權。
2. 在 hello 命令提示字元中輸入：
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. Hello cmdlet 順利完成之後，您會得到新的服務資料加密金鑰。 複製並儲存此金鑰，以供此程序的步驟 3 使用。 此金鑰將會使用所有剩餘 hello StorSimple Manager 服務註冊裝置的 hello tooupdate。
   
   > [!NOTE]
   > 此程序必須在授權 StorSimple 裝置後的四個小時內起始。
   > 
   > 
   
   這個新的金鑰，然後會傳送 toohello 服務推入 toobe tooall hello 登錄的裝置與 hello 服務。 Hello 服務儀表板上，即會出現警示。 hello 服務將會停用所有 hello hello 註冊裝置上的作業，hello 裝置系統管理員將必須 tooupdate hello 服務資料加密金鑰 hello 上的其他裝置。 不過，hello I/o （傳送資料 toohello 雲端的主機） 不會被中斷。
   
   如果您有單一裝置註冊 tooyour 服務 hello 變換程序現在已完成，可以略過 hello 下一個步驟。 如果您有多個裝置已註冊的 tooyour 服務時，繼續 toostep 3。

### <a name="step-3-update-hello-service-data-encryption-key-on-other-storsimple-devices"></a>步驟 3： 更新其他 StorSimple 裝置上的 hello 服務資料加密金鑰
如果您有多個裝置已註冊的 tooyour StorSimple Manager 服務，必須在您的 StorSimple 裝置 hello Windows PowerShell 介面中執行這些步驟。 您在步驟 2 中取得的 hello 金鑰必須使用的 tooupdate 所有 hello 剩餘 StorSimple 裝置向 StorSimple Manager 服務的 hello。

執行下列步驟 tooupdate hello 服務資料加密在裝置上的 hello。

#### <a name="tooupdate-hello-service-data-encryption-key"></a>tooupdate hello 服務資料加密金鑰
1. 使用 Windows PowerShell for StorSimple tooconnect toohello 主控台。 選取選項 1 toolog 上，具有完整存取權。
2. 在 hello 命令提示字元中輸入：
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. 提供 hello 服務資料加密金鑰，您在取得[步驟 2： 使用 Windows PowerShell for StorSimple tooinitiate hello 服務資料加密金鑰變更](#to-initiate-the-service-data-encryption-key-change)。


## <a name="next-steps"></a>後續步驟
* 深入了解 hello [StorSimple 部署程序](storsimple-8000-deployment-walkthrough-u2.md)。
* 深入了解 [管理 StorSimple 儲存體帳戶](storsimple-8000-manage-storage-accounts.md)。
* 深入了解如何太[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。
