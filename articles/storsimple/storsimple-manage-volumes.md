---
title: "aaaManage StorSimple 磁碟區 |Microsoft 文件"
description: "說明如何 tooadd、 修改、 監視及刪除 StorSimple 磁碟區，以及如何 tootake 它們只有在必要時離線。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ccabd859-590c-4568-a81d-6ff38f125be3
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/11/2016
ms.author: v-sharos
ms.openlocfilehash: 8dc646261ee2ad8f2b80291518716f4de55b63f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-volumes"></a>使用 hello StorSimple Manager 服務 toomanage 磁碟區
[!INCLUDE [storsimple-version-selector-manage-volumes](../../includes/storsimple-version-selector-manage-volumes.md)]

## <a name="overview"></a>概觀
本教學課程將說明 toouse hello StorSimple Manager 服務 toocreate 並管理 hello StorSimple 裝置和 StorSimple 虛擬裝置上的磁碟區。

hello StorSimple Manager 服務是 hello Azure 傳統入口網站，可讓您從單一 web 介面來管理您的 StorSimple 解決方案的延伸。 加法 toomanaging 磁碟區，您可以使用 hello StorSimple Manager 服務 toocreate 和管理 StorSimple 服務、 檢視和管理裝置、 檢視警示，以及檢視和管理備份原則與 hello 備份類別目錄。

> [!NOTE]
> Azure StorSimple 只能建立精簡佈建的磁碟區。 您無法在 Azure StorSimple 系統上建立完整佈建或部分佈建的磁碟區。
> 
> 精簡佈建是一種虛擬化技術，可用的存放裝置會出現 tooexceed 實體資源。 而是會預先保留足夠的儲存空間，Azure StorSimple 會使用精簡佈建 tooallocate 剛好足夠空間 toomeet 目前的需求。 hello 彈性本質的雲端儲存體促進這種方法，因為 Azure StorSimple 可以增加或減少雲端儲存體 toomeet 需求的變更。
> 
> 

## <a name="hello-volumes-page"></a>hello 磁碟區 頁面
hello**磁碟區**頁面可讓您 toomanage hello 存放磁碟區 hello 為啟動器 （伺服器） 的 Microsoft Azure StorSimple 裝置上佈建。 它會顯示您的 StorSimple 裝置的磁碟區的 hello 清單。

 ![磁碟區頁面](./media/storsimple-manage-volumes/HCS_VolumesPage.png)

磁碟區是由一系列屬性所組成：

* **名稱**– 描述性的名稱必須是唯一的可協助識別 hello 磁碟區。 這個名稱也可在您篩選特定磁碟區時用於監視報告。
* **狀態** – 可為連線或離線。 如果磁碟區離線，並不允許存取 toouse hello 磁碟區的可見 tooinitiators （伺服器）。
* **容量**– 指定 hello 多大的磁碟區時，看得見 hello 啟動器 （伺服器）。 容量指定 hello 的 hello 啟動器 （伺服器） 來儲存的資料量總計。 磁碟區採精簡佈建，而且會刪除重複的資料。 這表示您的裝置不會預先配置實體儲存容量在內部或 hello 雲端根據 tooconfigured 磁碟區容量。 配置及取用視 hello 磁碟區容量。
* **型別**– hello 磁碟區類型可以是階層式或封存 （其子型別的階層）
* **存取**– 指定允許存取 toothis 磁碟區的 hello 啟動器 （伺服器）。 不是成員的存取控制記錄 (ACR) 與 hello 磁碟區相關聯的啟動器不會看到 hello 磁碟區。
* **監視** – 指定是否正在監視磁碟區。 預設會在建立磁碟區時啟用監視。 不過，磁碟區複製會停用監視。 為磁碟區，監視 tooenable 遵循 hello 指示監視磁碟區。

hello 與磁碟區相關聯的最常見工作包括：

* 新增磁碟區
* 修改磁碟區
* 刪除磁碟區
* 使磁碟區離線
* 監視磁碟區

## <a name="add-a-volume"></a>新增磁碟區
您已在部署 StorSimple 方案期間 [建立磁碟區](storsimple-deployment-walkthrough-u1.md#step-6-create-a-volume) 。 新增磁碟區會是類似的程序。

### <a name="tooadd-a-volume"></a>tooadd 磁碟區
1. 在 [hello**裝置**頁面、 選取 hello 裝置、 按兩下，然後再按一下 hello**磁碟區容器**] 索引標籤。
2. 選取磁碟區容器，然後按一下箭號 hello hello 對應資料列 tooaccess hello 磁碟區與 hello 容器相關聯。
3. 按一下**新增**hello hello 頁底端。 hello 新增磁碟區精靈 會啟動。
   
     ![加入磁碟區精靈基本設定](./media/storsimple-manage-volumes/AddVolume1.png)
4. 在 [hello 新增磁碟區精靈] 中，在**基本設定**，不要遵循 hello:
   
   1. 輸入磁碟區的 [名稱]  。
   2. 指定 hello**佈建的容量**以 GB 或 TB 磁碟區。 hello 容量必須介於 1 GB 到 64 TB 之間的實體裝置。 hello 可以佈建 StorSimple 虛擬裝置上的磁碟區的最大容量為 30 TB。
   3. 選取 hello**使用類型**磁碟區。 如果您使用 hello 分層磁碟區，對於封存的資料，選取 hello**對於不常存取的封存資料，使用此磁碟區**核取方塊，變更您的磁碟區的 hello 重複資料刪除區塊大小 too512 KB。 如果您未選取此選項，hello 對應的階層式磁碟區會使用 64 KB 的區塊大小。 較大的重複資料刪除區塊大小可讓大型的封存資料 toohello 雲端的 hello 裝置 tooexpedite hello 傳輸。（分層磁碟區已之前稱為主要磁碟區）。
   4. 按一下 [hello] 箭號圖示![箭號圖示](./media/storsimple-manage-volumes/HCS_ArrowIcon.png)toogo toohello**其他設定**頁面。
      
        ![加入磁碟區精靈其他設定](./media/storsimple-manage-volumes/AddVolume2.png)
5. 在 [其他設定] 下，加入新的存取控制記錄 (ACR)：
   
   1. 從 hello 下拉式清單中選取存取控制記錄 (ACR)。 或者，您可以加入新的 ACR。 Acr 可讓您判斷哪些主機可以存取您的磁碟區比對的 hello 使用 hello 記錄中列出的主機 IQN。
   2. 我們建議您藉由選取 hello 啟用預設備份**啟用此磁碟區的預設備份**核取方塊。
   3. 按一下 [hello] 核取圖示 ![核取圖示](./media/storsimple-manage-volumes/HCS_CheckIcon.png) 以 hello toocreate hello 磁碟區指定的設定。

您新的磁碟區現在已準備好 toouse。

## <a name="modify-a-volume"></a>修改磁碟區
當您需要 tooexpand 它或變更 hello 存取 hello 的磁碟區的主機時，請修改磁碟區。

> [!IMPORTANT]
> * 如果您修改 hello hello 裝置上的磁碟區大小，hello 磁碟區大小需要 toobe hello 主控件上的變更。
> * 此處所述的 hello 主機端步驟適用於 Windows Server 2012 (2012R2)。 Linux 或其他主機作業系統的程序會有所不同。 修改 hello 執行另一個作業系統的主機上的磁碟區時，請參閱 tooyour 主機作業系統的指示。
> 
> 

### <a name="toomodify-a-volume"></a>toomodify 磁碟區
1. 在 [hello**裝置**頁面、 選取 hello 裝置、 按兩下，然後再按一下 hello**磁碟區容器**] 索引標籤。此頁面會列出以表格格式與 hello 裝置相關聯的所有 hello 磁碟區容器。
2. 選取磁碟區容器，然後按一下它 toodisplay hello hello 容器內的所有 hello 磁碟區清單。
3. 在 hello**磁碟區**頁面上選取的磁碟區，然後按一下**修改**。
4. 在 hello 修改磁碟區精靈 在**基本設定**，您可以 hello 下列：
   
   * 編輯 hello**名稱**和**類型**如果您想 toomodify 分層磁碟區的 tooan 封存磁碟區選取 hello**對於不常存取的封存資料，使用此磁碟區**核取方塊 toochange hello 重複資料刪除區塊大小的磁碟區 too512 KB。
   * 增加 hello**佈建的容量**。 hello**佈建的容量**只能增加。 您無法在磁碟區建立後予以壓縮。
     
     > [!NOTE]
     > 指派給 tooa 磁碟區之後，您無法變更 hello 磁碟區容器。
     > 
     > 
5. 在下**其他設定**，您可以 hello 下列：
   
   * 修改 hello Acr 提供 hello 磁碟區已離線。 Hello 磁碟區已上線時，如果您需要 tootake 它離線的第一個。 Toohello 中的步驟，請參閱[使磁碟區離線](#take-a-volume-offline)先前 toomodifying hello ACR。
   * Hello 磁碟區離線之後，請修改 Acr hello 清單。
     
     > [!NOTE]
     > 您無法變更 hello**啟用此磁碟區的預設備份**hello 磁碟區的選項。
     > 
     > 
6. 按一下 hello 核取圖示以儲存您的變更 ![核取圖示](./media/storsimple-manage-volumes/HCS_CheckIcon.png). hello Azure 傳統入口網站將會顯示更新的磁碟區訊息。 已成功更新 hello 磁碟區時，它會顯示成功訊息。
7. 如果您要擴充磁碟區，完成下列步驟在您的 Windows 主機電腦上的 hello:
   
   1. 跳過**電腦管理** ->**磁碟管理**。
   2. 以滑鼠右鍵按一下 [磁碟管理]，並選取 [重新掃描磁碟]。
   3. 在 hello 清單中的磁碟，選取您更新的 hello 磁碟區、 按一下滑鼠右鍵，然後選取**延伸磁碟區**。 hello 延伸磁碟區精靈 隨即啟動。 按一下 [下一步] 。
   4. 完成 hello 精靈，接受 hello 的預設值。 Hello 精靈完成後，hello 磁碟區應該會顯示 hello 增加大小。

![提供的影片](./media/storsimple-manage-volumes/Video_icon.png) **提供的影片**

toowatch 的視訊示範，如何 tooexpand 磁碟區，按一下[這裡](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/)。

## <a name="take-a-volume-offline"></a>使磁碟區離線
您可能需要 tootake 磁碟區離線，當您計劃 toomodify 它或刪除它。 當磁碟區離線時，即無法進行讀寫存取。 您將需要 tootake hello 磁碟區離線 hello 裝置以及 hello 主機上。 執行下列步驟 tootake 磁碟區離線 hello。

### <a name="tootake-a-volume-offline"></a>tootake 磁碟區離線
1. 請確定有問題的 hello 磁碟區不是使用中，再將其離線。
2. Hello 主機上的 hello 磁碟區離線讓第一次。 這可免除 hello 磁碟區上的資料損毀的任何潛在風險。 如需特定步驟，請參閱主機作業系統的 toohello 指示。
3. Hello 主機已離線後，採用的離線 hello 裝置 hello 磁碟區，藉由執行下列步驟的 hello:
   
   1. 在 hello**裝置**頁面、 選取 hello 裝置、 按兩下，然後再按一下 hello**磁碟區容器** 索引標籤 hello**磁碟區容器**索引標籤上列出所有以表格格式hello 與 hello 裝置相關聯的磁碟區容器。
   2. 選取磁碟區容器，然後按一下它 toodisplay hello hello 容器內的所有 hello 磁碟區清單。
   3. 選取磁碟區，然後按一下 [離線] 。
   4. 系統提示您進行確認時，按一下 [是] 。 hello 磁碟區現在應該可以離線。
      
      磁碟區離線後，hello**上線**選項就會變成可用。

> [!NOTE]
> hello**離線**命令會傳送要求 toohello 裝置 tootake hello 磁碟區離線。 如果主機仍在使用 hello 磁碟區，這會導致連線中斷，但離線 hello 磁碟區將不會失敗。
> 
> 

## <a name="delete-a-volume"></a>刪除磁碟區
> [!IMPORTANT]
> 只有當磁碟區離線時，您才能予以刪除。
> 
> 

完成下列步驟 toodelete 磁碟區的 hello。

### <a name="toodelete-a-volume"></a>toodelete 磁碟區
1. 在 [hello**裝置**頁面、 選取 hello 裝置、 按兩下，然後再按一下 hello**磁碟區容器**] 索引標籤。
2. 選取您想要 toodelete hello 磁碟區的 hello 磁碟區容器。 按一下 hello 磁碟區容器 tooaccess hello**磁碟區**頁面。
3. 與這個容器相關聯的所有 hello 磁碟區會以表格格式都顯示。 檢查 hello 狀態想 toodelete hello 磁碟區。 如果您想要 toodelete hello 磁碟區未離線，使其離線的第一個步驟，下列 hello 步驟[使磁碟區離線](#take-a-volume-offline)。
4. Hello 磁碟區離線後，請按一下**刪除**hello hello 頁底端。
5. 系統提示您進行確認時，按一下 [是] 。 hello 磁碟區現在將會刪除與 hello**磁碟區**頁面會顯示更新的 hello hello 容器內的磁碟區清單。

## <a name="monitor-a-volume"></a>監視磁碟區
磁碟區監視可讓您的磁碟區的 toocollect 我 I/O 相關統計資料。 預設值為 hello 會啟用監視您所建立的前 32 磁碟區。 預設會停用監視其他磁碟區。 預設也會停用監視複製的磁碟區。

執行下列步驟 tooenable hello 或停用磁碟區的監視。

### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable 或停用磁碟區監視
1. 在 [hello**裝置**頁面、 選取 hello 裝置、 按兩下，然後再按一下 hello**磁碟區容器**] 索引標籤。
2. 選取哪些 hello 磁碟區所在，hello 磁碟區容器，然後按一下hello 磁碟區容器 tooaccess hello**磁碟區**頁面。
3. 與這個容器相關聯的所有 hello 磁碟區會都列在 hello 表格式顯示中。 按一下並選取 hello 磁碟區或磁碟區再製。
4. 在 hello hello 頁面底部，按一下**修改**。
5. 在 hello 修改磁碟區精靈 在**基本設定**，選取**啟用**或**停用**從 hello**監視**下拉式清單。
   
    ![修改磁碟區基本設定](./media/storsimple-manage-volumes/HCS_MonitorVolumeM.png)

## <a name="next-steps"></a>後續步驟
* 了解如何太[複製 StorSimple 磁碟區](storsimple-clone-volume.md)。
* 了解如何太[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。

