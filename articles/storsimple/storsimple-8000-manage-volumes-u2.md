---
title: "aaaManage StorSimple 磁碟區 (Update 3) |Microsoft 文件"
description: "說明如何 tooadd、 修改、 監視及刪除 StorSimple 磁碟區，以及如何 tootake 它們只有在必要時離線。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 6228c4486dd5a7887df670c4c4584c4edcdfc509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-volumes-update-3-or-later"></a>使用 hello StorSimple 裝置管理員服務 toomanage 磁碟區 (Update 3 或更新版本)

## <a name="overview"></a>概觀

本教學課程將說明 toouse hello StorSimple 裝置管理員服務 toocreate 並管理執行 Update 3 及更新版本的 hello StorSimple 8000 系列裝置上的磁碟區。

hello StorSimple 裝置管理員服務是 hello Azure 入口網站，可讓您從單一 web 介面來管理您的 StorSimple 解決方案中的延伸模組。 所有裝置上使用 hello Azure 入口網站 toomanage 磁碟區。 您也可以建立和管理 StorSimple 服務、管理裝置、備份原則，以及備份類別目錄，並檢視警示。

## <a name="volume-types"></a>磁碟區類型

StorSimple 磁碟區可以是：

* **固定在本機磁碟區**： 隨時都能在這些磁碟區中的資料會保留在 hello 本機 StorSimple 裝置。
* **分層磁碟區**： 這些磁碟區中的資料可以 spill toohello 雲端。

封存的磁碟區是一種分層磁碟區。 hello 較大重複資料刪除區塊大小用於封存磁碟區，可讓資料 toohello 雲端的 hello 裝置 tootransfer 較區段。

如有必要，您可以變更 hello 磁碟區類型從本機 tootiered 或階層式 toolocal。 如需詳細資訊，請移至太[變更 hello 磁碟區類型](#change-the-volume-type)。

### <a name="locally-pinned-volumes"></a>固定在本機的磁碟區

本機固定磁碟區是不層資料 toohello 雲端的完整佈建磁碟區，以確保本機可保證，針對主要資料，獨立於雲端連線。 固定在本機的磁碟區的資料不會進行重複資料刪除和壓縮，但是，固定在本機的磁碟區的快照會進行重複資料刪除。 

固定在本機的磁碟區是完整佈建，因此，當您建立它們時，必須在裝置上有足夠的空間。 您可以佈建本機固定磁碟區總 tooa hello StorSimple 8100 裝置上為 8 TB 和 20 TB hello 8600 裝置上的大小上限。 StorSimple 會保留 hello 剩餘本機裝置上的空間 hello 快照集、 中繼資料，以及資料處理。 您可以增加 hello 的本機固定磁碟區 toohello 最大可用空間的大小，但您無法減少 hello 一次建立的磁碟區大小。

當您建立本機固定磁碟區時，則會減少 hello 建立分層磁碟區的可用空間。 hello 反向也是如此： 如果您有現有的階層式磁碟區時，會低於 hello 最大限制上述 hello 空間可供建立本機固定磁碟區。 如需有關本機磁碟區的詳細資訊，請參閱 toohello[本機固定磁碟區上的常見問題集](storsimple-8000-local-volume-faq.md)。

### <a name="tiered-volumes"></a>分層磁碟區

階層式磁碟區是在哪一個 hello 經常存取的資料會保持在 hello 裝置上的本機和較不常用資料，則會自動分層 toohello 雲端的精簡佈建磁碟區。 精簡佈建是一種虛擬化技術，可用的存放裝置會出現 tooexceed 實體資源。 而是會預先保留足夠的儲存空間，StorSimple 會使用精簡佈建 tooallocate 剛好足夠空間 toomeet 目前的需求。 hello 彈性本質的雲端儲存體促進這種方法，因為 StorSimple 可以增加或減少雲端儲存體 toomeet 需求的變更。

如果您使用 hello 分層磁碟區的封存資料，選取 hello**對於不常存取的封存資料，使用此磁碟區**核取方塊 toochange hello 重複資料刪除區塊大小的磁碟區 too512 KB。 如果您未選取此選項，hello 對應的階層式磁碟區會使用 64 KB 的區塊大小。 較大的重複資料刪除區塊大小可讓大型的封存資料 toohello 雲端的 hello 裝置 tooexpedite hello 傳輸。


### <a name="provisioned-capacity"></a>佈建的容量

請參閱下表針對每個裝置和磁碟區類型的最大佈建的容量 toohello。 (請注意，固定在本機的磁碟區無法在虛擬裝置上使用。)

|  | 最大的分層磁碟區大小 | 最大的固定在本機的磁碟區大小 |
| --- | --- | --- |
| **實體裝置** | | |
| 8100 |64 TB |8 TB |
| 8600 |64 TB |20 TB |
| **虛擬裝置** | | |
| 8010 |30 TB |N/A |
| 8020 |64 TB |N/A |

## <a name="hello-volumes-blade"></a>hello 磁碟區 刀鋒視窗

hello**磁碟區**刀鋒視窗可讓您 toomanage hello 存放磁碟區 hello 為啟動器 （伺服器） 的 Microsoft Azure StorSimple 裝置上佈建。 它會顯示 hello StorSimple 裝置連線的 tooyour 服務 hello 的磁碟區的清單。

 ![磁碟區頁面](./media/storsimple-8000-manage-volumes-u2/volumeslist.png)

磁碟區是由一系列屬性所組成：

* **磁碟區名稱**– 描述性的名稱必須是唯一的可協助識別 hello 磁碟區。 這個名稱也可在您篩選特定磁碟區時用於監視報告。 一旦建立 hello 磁碟區，但無法重新命名。
* **狀態** – 可為連線或離線。 如果磁碟區已離線，就不允許存取 toouse hello 磁碟區的可見 tooinitiators （伺服器）。
* **容量**– 指定 hello 的 hello 啟動器 （伺服器） 來儲存的資料量總計。 固定在本機磁碟區完全佈建，而且位於 hello StorSimple 裝置上。 精簡佈建分層磁碟區和 hello 資料重複資料刪除。 使用精簡佈建磁碟區，您的裝置不會預先配置實體儲存容量在內部或根據 tooconfigured 磁碟區容量的 hello 雲端。 配置及取用視 hello 磁碟區容量。
* **型別**– 指出 hello 磁碟區是否為**分層**(hello 預設) 或**固定在本機**。

使用 hello 指示在本教學課程 tooperform hello，下列工作：

* 新增磁碟區 
* 修改磁碟區 
* 變更 hello 磁碟區類型
* 刪除磁碟區 
* 使磁碟區離線 
* 監視磁碟區 

## <a name="add-a-volume"></a>新增磁碟區

您已在部署 StorSimple 8000 系列裝置期間[建立磁碟區](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume)。 新增磁碟區會是類似的程序。

#### <a name="tooadd-a-volume"></a>tooadd 磁碟區

1. 從 hello 表格清單中的 hello 裝置 hello**裝置**刀鋒視窗中，選取您的裝置。 按一下 [+ 新增磁碟區]。

    ![新增磁碟區](./media/storsimple-8000-manage-volumes-u2/step5createvol1.png)

2. 在 hello**加入磁碟區**刀鋒視窗中：
   
    1. hello**選取裝置**欄位會自動填入您目前的裝置。

    2. 從 hello 下拉式清單中，選取 hello 磁碟區容器，您需要 tooadd 磁碟區。

    3.  輸入磁碟區的 [名稱]  。 Hello 磁碟區建立之後，您無法重新命名 hello 磁碟區。

    4. 在 hello 下拉式清單中，選取 hello**類型**磁碟區。 需要本機保證、低延遲，以及高效能的工作負載，請選取 [固定在本機]  磁碟區。 針對所有其他資料，請選取 [分層]  磁碟區。 如果您將此磁碟區用於封存資料，請核取 [將此磁碟區用於較不常存取的封存資料] 核取方塊。
      
       分層磁碟區已精簡佈建，而且可以快速地建立。 選取**對於不常存取的封存資料，使用此磁碟區**封存資料變更 hello 重複資料刪除區塊大小的磁碟區為目標的階層式磁碟區 too512 KB。 如果未核取此欄位，hello 對應的階層式磁碟區會使用 64 KB 的區塊大小。 較大的重複資料刪除區塊大小可讓大型的封存資料 toohello 雲端的 hello 裝置 tooexpedite hello 傳輸。
       
       本機固定磁碟區以佈建，並確保維持本機 toohello 裝置 hello hello 磁碟區上的主要資料，並不 spill toohello 雲端。  如果您建立本機固定磁碟區，hello 裝置檢查 hello 本機層上的可用空間的 hello tooprovision hello 大量要求的大小。 建立本機固定磁碟區的 hello 作業可能會溢出 hello 裝置 toohello 雲端的現有資料並採取 toocreate hello 磁碟區的 hello 時間可能較長。 hello 總時間取決於 hello 大小 hello 佈建磁碟區、 可用的網路頻寬及裝置上的 hello 資料。

    5. 指定 hello**佈建的容量**磁碟區。 記下的 hello 容量可根據選取的 hello 磁碟區類型。 hello 指定磁碟區大小不能超過 hello 可用空間。
      
       您可以佈建本機固定磁碟區總 too8.5 TB 或向上 too200 TB hello 8100 裝置上的階層式磁碟區。 您可以在較大 8600 裝置 hello，佈建本機固定磁碟區總 too22.5 TB 或分層的磁碟區總 too500 TB。 因為 hello 裝置上的本機空間是必要的 toohost hello 工作組的階層式磁碟區，建立本機固定磁碟區會影響 hello 空間可供佈建分層磁碟區。 因此，如果您建立固定在本機的磁碟區，建立分層磁碟區的可用空間就會縮小。 同樣地，如果建立為分層磁碟區時，就會降低 hello 的可用空間來建立本機固定磁碟區。
      
       8100 裝置上佈建 8.5 TB （最大容許大小） 的本機固定磁碟區，如果您已耗盡所有 hello 本機上的可用空間 hello 裝置。 您無法建立任何階層式磁碟區從該點以後 hello 裝置 toohost hello 工作集 hello 上沒有本機空間分層磁碟區。 現有的階層式磁碟區也會影響 hello 的可用空間。 例如，如果您的 8100 裝置已經有大約 106 TB 的分層磁碟區，則固定在本機的磁碟區僅只有 4 TB 的可用空間。

    6. 在 hello**連線主機**欄位中，按一下 hello 箭號。 

        ![已連線的主機](./media/storsimple-8000-manage-volumes-u2/step5createvol2.png)

    7. 在 hello**連線主機**刀鋒視窗中，選擇現有的 ACR，或加入新的 ACR。 如果您選擇新的 ACR，然後提供**名稱**acr，提供 hello **iSCSI Qualified Name** (IQN) 的 Windows 主機。 如果您沒有 hello IQN，請移至太[Get hello Windows Server 主機的 IQN](#get-the-iqn-of-a-windows-server-host)。 按一下 [建立] 。 以指定的 hello 建立磁碟區設定。

        ![Click Create](./media/storsimple-8000-manage-volumes-u2/step5createvol3.png)

您新的磁碟區現在已準備好 toouse。

> [!NOTE]
> 如果您建立本機固定磁碟區，然後再建立另一部本機固定磁碟區，立即 hello 磁碟區建立工作之後，以循序方式執行。 hello 第一個磁碟區建立作業必須完成才能開始進行 hello 下一個磁碟區建立工作。

## <a name="modify-a-volume"></a>修改磁碟區

當您需要 tooexpand 它或變更 hello 存取 hello 的磁碟區的主機時，請修改磁碟區。

> [!IMPORTANT]
> * 如果您修改 hello hello 裝置上的磁碟區大小，hello 磁碟區大小需要 toobe hello 主控件上的變更。
> * 此處所述的 hello 主機端步驟適用於 Windows Server 2012 (2012R2)。 Linux 或其他主機作業系統的程序會有所不同。 修改 hello 執行另一個作業系統的主機上的磁碟區時，請參閱 tooyour 主機作業系統的指示。

#### <a name="toomodify-a-volume"></a>toomodify 磁碟區

1. 在 tooyour StorSimple 裝置管理員服務的 **裝置**。 從 hello 表格清單中的 hello 裝置，選取您想 toomodify hello 磁碟區的 hello 裝置。 按一下 [設定] > [磁碟區]。

    ![移 tooVolumes 刀鋒視窗](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

2. 從 hello 表格式的磁碟區清單，選取 hello 磁碟區，然後 tooinvoke hello 操作功能表上按一下滑鼠右鍵。 選取**離線**tootake hello 磁碟區離線，您將修改。

    ![選取並讓磁碟區離線](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. 在 hello**離線**刀鋒視窗中，檢閱 hello 影響 hello 磁碟區離線，並選取 hello 對應的核取方塊。 請確認 hello hello 主機上的對應磁碟區離線第一次。 如需如何 tootake 離線的磁碟區在主機伺服器上連接 tooStorSimple 資訊，請參閱 toooperating 系統的特定指示。 按一下 [離線]。

    ![檢閱讓磁碟區離線的影響](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

4. Hello 磁碟區已離線 （如所示 hello 磁碟區狀態） 之後，選擇 hello 磁碟區，然後以滑鼠右鍵按一下 tooinvoke hello 操作功能表。 選取 [修改磁碟區]。

    ![選取 [修改磁碟區]](./media/storsimple-8000-manage-volumes-u2/modifyvol9.png)


5. 在 hello**修改磁碟區**刀鋒視窗中，您可以進行下列變更 hello:
   
   1. hello 磁碟區**名稱**無法編輯。
   2. 轉換 hello**類型**從本機固定 tootiered 或釘選的分層式 toolocally (請參閱[變更 hello 磁碟區類型](#change-the-volume-type)如需詳細資訊)。
   3. 增加 hello**佈建的容量**。 hello**佈建的容量**只能增加。 您無法在磁碟區建立後予以壓縮。
   4. 在下**連線主機**，您可以修改 hello ACR。 toomodify ACR，hello 磁碟區必須處於離線狀態。

       ![檢閱讓磁碟區離線的影響](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

5. 按一下**儲存**toosave 您的變更。 系統提示您進行確認時，按一下 [是] 。 hello Azure 入口網站將會顯示更新的磁碟區訊息。 已成功更新 hello 磁碟區時，它會顯示成功訊息。

    ![檢閱讓磁碟區離線的影響](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

7. 如果您要擴充磁碟區，完成下列步驟在您的 Windows 主機電腦上的 hello:
   
   1. 跳過**電腦管理** ->**磁碟管理**。
   2. 以滑鼠右鍵按一下 [磁碟管理]，並選取 [重新掃描磁碟]。
   3. 在 hello 清單中的磁碟，選取您更新的 hello 磁碟區、 按一下滑鼠右鍵，然後選取**延伸磁碟區**。 hello 延伸磁碟區精靈 隨即啟動。 按一下 [下一步] 。
   4. 完成 hello 精靈，接受 hello 的預設值。 Hello 精靈完成後，hello 磁碟區應該會顯示 hello 增加大小。
      
      > [!NOTE]
      > 如果您展開本機固定磁碟區，然後展開本機另一個 hello 磁碟區延伸作業之後，以循序方式執行，請立即固定磁碟區。 hello 第一個磁碟區擴充工作必須完成才能開始進行下一個磁碟區擴充工作 hello。
      

## <a name="change-hello-volume-type"></a>變更 hello 磁碟區類型

您可以變更 hello 磁碟區類型從分層式 toolocally 釘選，或從本機固定 tootiered。 不過，這種轉換不應該經常發生。

### <a name="tiered-toolocal-volume-conversion-considerations"></a>階層式的 toolocal 磁碟區轉換考量

某些階層式 toolocally 釘選的轉換磁碟區的原因如下：

* 關於資料可用性和效能的本機保證
* 消除雲端延遲和雲端連線問題。

一般來說，這些是小型經常想 tooaccess 的現有磁碟區。 當固定在本機的磁碟區建立時，它就會完整佈建。 

如果您想要轉換的階層式磁碟區 tooa 固定在本機磁碟區，StorSimple 會確認您在裝置上有足夠的空間，開始 hello 轉換之前。 如果您有足夠的空間，您會收到錯誤，且會取消 hello 作業。 

> [!NOTE]
> 開始從釘選的分層式 toolocally 轉換之前，請確定您考慮 hello 空間需求的其他工作負載。 

從階層式的 tooa 固定在本機磁碟區的轉換可能會影響裝置的效能。 此外，hello 下列因素可能會增加 hello toocomplete hello 轉換所花費的時間：

* 頻寬不足。
* 沒有最新備份。

這些因素可能會有的 toominimize hello 效果：

* 請檢閱頻寬節流設定原則，並確認有專用的 40 Mbps 頻寬。
* 排程離峰時間的 hello 轉換。
* 在開始 hello 轉換之前，請建立的雲端快照。

如果您想要轉換多個磁碟區 （支援不同的工作負載），您應該設定 hello 磁碟區轉換優先權，優先權較高的磁碟區會先轉換。 例如，您應該先轉換裝載虛擬機器 (VM) 的磁碟區，或具有 SQL 工作負載的磁碟區，然後才轉換檔案共用工作負載的磁碟區。

### <a name="local-tootiered-volume-conversion-considerations"></a>本機 tootiered 磁碟區轉換考量

您可以在本機固定磁碟區 tooa toochange 分層磁碟區如果您需要額外的空間 tooprovision 其他磁碟區。 當您轉換 hello 固定在本機磁碟區 tootiered 時，hello hello 釋出容量大小會增加 hello hello 裝置上的可用容量。 如果連線問題會使磁碟區的 hello 轉換從 hello 區域型別 toohello 層型別，hello 本機磁碟區會展示分層磁碟區的內容之前 hello 轉換已完成。 這是因為某些資料可能會溢出 toohello 雲端。 此餘力的資料會繼續 toooccupy hello 作業會重新啟動時，完成之前無法釋放的 hello 裝置上的本機空間。

> [!NOTE]
> 轉換磁碟區可能需要一些時間，且您在啟動之後無法取消轉換。 hello 磁碟區仍在進行 hello 轉換時，線上和才能進行備份，但您無法展開或 hello 轉換正在進行時，還原 hello 磁碟區。


#### <a name="toochange-hello-volume-type"></a>toochange hello 磁碟區類型

1. 在 tooyour StorSimple 裝置管理員服務的 **裝置**。 從 hello 表格清單中的 hello 裝置，選取您想 toomodify hello 磁碟區的 hello 裝置。 按一下 [設定] > [磁碟區]。

    ![移 tooVolumes 刀鋒視窗](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. 從 hello 表格式的磁碟區清單，選取 hello 磁碟區，然後 tooinvoke hello 操作功能表上按一下滑鼠右鍵。 選取 [修改]。

    ![從操作功能表選取 [修改]](./media/storsimple-8000-manage-volumes-u2/changevoltype2.png)

4. 在 hello**修改磁碟區**刀鋒視窗中，變更 hello 磁碟區類型從 hello 選取 hello 新類型**類型**下拉式清單。
   
   * 如果您要變更 hello 類型太**固定在本機**，StorSimple 會檢查 toosee，如果沒有足夠的容量。
   * 如果您要變更 hello 類型太**分層**及此磁碟區會用於封存資料，選取 hello**對於不常存取的封存資料，使用此磁碟區**核取方塊。
   * 如果您要設定本機固定磁碟區，如層或_反之亦然_，hello 會出現下列訊息。
   
    ![變更磁碟區類型訊息](./media/storsimple-8000-manage-volumes-u2/changevoltype3.png)

7. 按一下**儲存**toosave hello 變更。 當提示確認，請按一下**是**toostart hello 轉換程序。 

    ![儲存並確認](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

8. hello Azure 入口網站會顯示 hello 建立工作，會更新 hello 磁碟區的通知。 按一下 hello 通知 toomonitor hello 狀態 hello 磁碟區轉換工作。

    ![磁碟區轉換作業](./media/storsimple-8000-manage-volumes-u2/changevoltype5.png)

## <a name="take-a-volume-offline"></a>使磁碟區離線

當您計劃 toomodify 或刪除 hello 磁碟區時，您可能需要 tootake 磁碟區離線。 當磁碟區離線時，即無法進行讀寫存取。 您必須採取 hello 上的磁碟區離線 hello 主機和 hello 裝置。

#### <a name="tootake-a-volume-offline"></a>tootake 磁碟區離線

1. 請確定有問題的 hello 磁碟區不是使用中，再將其離線。
2. Hello 主機上的 hello 磁碟區離線讓第一次。 這可免除 hello 磁碟區上的資料損毀的任何潛在風險。 如需特定步驟，請參閱主機作業系統的 toohello 指示。
3. Hello 主機已離線後，採用的離線 hello 裝置 hello 磁碟區，藉由執行下列步驟的 hello:
   
    1. 在 tooyour StorSimple 裝置管理員服務的 **裝置**。 從 hello 表格清單中的 hello 裝置，選取您想 toomodify hello 磁碟區的 hello 裝置。 按一下 [設定] > [磁碟區]。

        ![移 tooVolumes 刀鋒視窗](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

    2. 從 hello 表格式的磁碟區清單，選取 hello 磁碟區，然後 tooinvoke hello 操作功能表上按一下滑鼠右鍵。 選取**離線**tootake hello 磁碟區離線，您將修改。

        ![選取並讓磁碟區離線](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. 在 hello**離線**刀鋒視窗中，檢閱 hello 影響 hello 磁碟區離線，並選取 hello 對應的核取方塊。 按一下 [離線]。 

    ![檢閱讓磁碟區離線的影響](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)
      
      Hello 磁碟區離線時，會通知您。 hello 磁碟區狀態也會更新 tooOffline。
      
4. 磁碟區離線，如果您選取 hello 磁碟區並按一下滑鼠右鍵後,**上線**hello 內容功能表中的選項可用。

> [!NOTE]
> hello**離線**命令會傳送要求 toohello 裝置 tootake hello 磁碟區離線。 如果主機仍在使用 hello 磁碟區，這會導致連線中斷，但離線 hello 磁碟區將不會失敗。

## <a name="delete-a-volume"></a>刪除磁碟區

> [!IMPORTANT]
> 只有當磁碟區離線時，您才能予以刪除。

完成下列步驟 toodelete 磁碟區的 hello。

#### <a name="toodelete-a-volume"></a>toodelete 磁碟區

1. 在 tooyour StorSimple 裝置管理員服務的 **裝置**。 從 hello 表格清單中的 hello 裝置，選取您想 toomodify hello 磁碟區的 hello 裝置。 按一下 [設定] > [磁碟區]。

    ![移 tooVolumes 刀鋒視窗](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. 檢查 hello 狀態想 toodelete hello 磁碟區。 如果您想要 toodelete hello 磁碟區未離線，先使其離線。 中的 hello 步驟[使磁碟區離線](#take-a-volume-offline)。
4. Hello 磁碟區離線後，選取 hello 磁碟區、 tooinvoke hello 操作功能表上按一下滑鼠右鍵，然後選取**刪除**。

    ![從操作功能表選取 [刪除]](./media/storsimple-8000-manage-volumes-u2/deletevol1.png)

5. 在 hello**刪除**刀鋒視窗中，檢閱和選取 hello 針對 hello 影響刪除磁碟區的核取方塊。 當您刪除磁碟區時，位於 hello 磁碟區的所有 hello 資料都會遺失。 

    ![儲存並確認變更](./media/storsimple-8000-manage-volumes-u2/deletevol2.png)

6. 刪除 hello 磁碟區之後，更新 tooindicate hello 刪除磁碟區 hello 表格式清單。

    ![更新磁碟區清單](./media/storsimple-8000-manage-volumes-u2/deletevol3.png)
   
   > [!NOTE]
   > 如果您刪除本機固定磁碟區，可能不會立即更新 hello 空間供新磁碟區。 hello StorSimple 裝置管理員服務會定期更新 hello 可用的本機空間。 我們建議您等待幾分鐘的時間再 toocreate hello 新磁碟區。
   >
   > 此外，如果您刪除本機固定磁碟區，然後再刪除另一部本機固定磁碟區，立即 hello 大量刪除作業之後，以循序方式執行。 hello 第一個磁碟區刪除工作必須完成才能開始進行下一個磁碟區刪除工作 hello。

## <a name="monitor-a-volume"></a>監視磁碟區

磁碟區監視可讓您的磁碟區的 toocollect 我 I/O 相關統計資料。 預設值為 hello 會啟用監視您所建立的前 32 磁碟區。 預設會停用監視其他磁碟區。 

> [!NOTE]
> 預設會停用監視複製的磁碟區。


執行下列步驟 tooenable hello 或停用磁碟區的監視。

#### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable 或停用磁碟區監視

1. 在 tooyour StorSimple 裝置管理員服務的 **裝置**。 從 hello 表格清單中的 hello 裝置，選取您想 toomodify hello 磁碟區的 hello 裝置。 按一下 [設定] > [磁碟區]。
2. 從 hello 表格式的磁碟區清單，選取 hello 磁碟區，然後 tooinvoke hello 操作功能表上按一下滑鼠右鍵。 選取 [修改]。
3. 在 hello**修改磁碟區**刀鋒視窗中，針對**監視**選取**啟用**或**停用**tooenable 或停用監視。

    ![停用監視](./media/storsimple-8000-manage-volumes-u2/monitorvol1.png) 

4. 按一下 [儲存]，當系統提示您進行確認時，按一下 [是]。 hello Azure 入口網站會顯示 hello 磁碟區已成功更新之後更新 hello 磁碟區，然後成功訊息的通知。

## <a name="next-steps"></a>後續步驟

* 了解如何太[複製 StorSimple 磁碟區](storsimple-8000-clone-volume-u2.md)。
* 了解如何太[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。

