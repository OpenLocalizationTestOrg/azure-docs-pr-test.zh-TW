---
title: "aaaManage StorSimple 磁碟區 (U2) |Microsoft 文件"
description: "說明如何 tooadd、 修改、 監視及刪除 StorSimple 磁碟區，以及如何 tootake 它們只有在必要時離線。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 57896932-0aa5-4805-970c-d13403ae7551
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 10/28/2016
ms.author: alkohli
ms.openlocfilehash: 8b64f1d92023646cdf881882854d9bc5d7334a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-volumes-update-2"></a>使用 hello StorSimple Manager 服務 toomanage 磁碟區 (Update 2)
[!INCLUDE [storsimple-version-selector-manage-volumes](../../includes/storsimple-version-selector-manage-volumes.md)]

## <a name="overview"></a>概觀
本教學課程將說明 toouse hello StorSimple Manager 服務 toocreate 並安裝 Update 2 中管理 hello StorSimple 裝置和 StorSimple 虛擬裝置上的磁碟區。

hello StorSimple Manager 服務是 hello Azure 傳統入口網站，可讓您從單一 web 介面來管理您的 StorSimple 解決方案中的延伸模組。 加法 toomanaging 磁碟區，您可以使用 hello StorSimple Manager 服務 toocreate 和管理 StorSimple 服務、 檢視和管理裝置、 檢視警示，以及檢視和管理備份原則與 hello 備份類別目錄。

## <a name="volume-types"></a>磁碟區類型
StorSimple 磁碟區可以是：

* **固定在本機磁碟區**： 隨時都能在這些磁碟區中的資料會保留在 hello 本機 StorSimple 裝置。
* **分層磁碟區**： 這些磁碟區中的資料可以 spill toohello 雲端。

封存的磁碟區是一種分層磁碟區。 hello 較大重複資料刪除區塊大小用於封存磁碟區，可讓資料 toohello 雲端的 hello 裝置 tootransfer 較區段。 

如有必要，您可以變更 hello 磁碟區類型從本機 tootiered 或階層式 toolocal。 如需詳細資訊，請移至太[變更 hello 磁碟區類型](#change-the-volume-type)。

### <a name="locally-pinned-volumes"></a>固定在本機的磁碟區
本機固定磁碟區是不層資料 toohello 雲端的完整佈建磁碟區，以確保本機可保證，針對主要資料，獨立於雲端連線。 固定在本機的磁碟區的資料不會進行重複資料刪除和壓縮，但是，固定在本機的磁碟區的快照會進行重複資料刪除。 

固定在本機的磁碟區是完整佈建，因此，當您建立它們時，必須在裝置上有足夠的空間。 您可以佈建本機固定磁碟區總 tooa hello StorSimple 8100 裝置上為 8 TB 和 20 TB hello 8600 裝置上的大小上限。 StorSimple 會保留 hello 剩餘本機裝置上的空間 hello 快照集、 中繼資料，以及資料處理。 您可以增加 hello 的本機固定磁碟區 toohello 最大可用空間的大小，但您無法減少 hello 一次建立的磁碟區大小。

當您建立本機固定磁碟區時，則會減少 hello 建立分層磁碟區的可用空間。 hello 反向也是如此： 如果您有現有的階層式磁碟區時，會低於 hello 最大限制上述 hello 空間可供建立本機固定磁碟區。 如需有關本機磁碟區的詳細資訊，請參閱 toohello[本機固定磁碟區上的常見問題集](storsimple-local-volume-faq.md)。   

### <a name="tiered-volumes"></a>分層磁碟區
階層式磁碟區是在哪一個 hello 經常存取的資料會保持在 hello 裝置上的本機和較不常用資料，則會自動分層 toohello 雲端的精簡佈建磁碟區。 精簡佈建是一種虛擬化技術，可用的存放裝置會出現 tooexceed 實體資源。 而是會預先保留足夠的儲存空間，StorSimple 會使用精簡佈建 tooallocate 剛好足夠空間 toomeet 目前的需求。 hello 彈性本質的雲端儲存體促進這種方法，因為 StorSimple 可以增加或減少雲端儲存體 toomeet 需求的變更。

如果您使用 hello 分層磁碟區，對於封存的資料，選取 hello**對於不常存取的封存資料，使用此磁碟區**核取方塊，變更您的磁碟區的 hello 重複資料刪除區塊大小 too512 KB。 如果您未選取此選項，hello 對應的階層式磁碟區會使用 64 KB 的區塊大小。 較大的重複資料刪除區塊大小可讓大型的封存資料 toohello 雲端的 hello 裝置 tooexpedite hello 傳輸。

> [!NOTE]
> 保存與 StorSimple 更新前 2 版本所建立的磁碟區將會匯入為階層式 hello 選取保存核取方塊。
> 
> 

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

## <a name="hello-volumes-page"></a>hello 磁碟區 頁面
hello**磁碟區**頁面可讓您 toomanage hello 存放磁碟區 hello 為啟動器 （伺服器） 的 Microsoft Azure StorSimple 裝置上佈建。 它會顯示您的 StorSimple 裝置的磁碟區的 hello 清單。

 ![磁碟區頁面](./media/storsimple-manage-volumes-u2/VolumePage.png)

磁碟區是由一系列屬性所組成：

* **磁碟區名稱**– 描述性的名稱必須是唯一的可協助識別 hello 磁碟區。 這個名稱也可在您篩選特定磁碟區時用於監視報告。
* **狀態** – 可為連線或離線。 如果磁碟區已離線，就不允許存取 toouse hello 磁碟區的可見 tooinitiators （伺服器）。
* **容量**– 指定 hello 的 hello 啟動器 （伺服器） 來儲存的資料量總計。 固定在本機磁碟區完全佈建，而且位於 hello StorSimple 裝置上。 精簡佈建分層磁碟區和 hello 資料重複資料刪除。 使用精簡佈建磁碟區，您的裝置不會預先配置實體儲存容量在內部或根據 tooconfigured 磁碟區容量的 hello 雲端。 配置及取用視 hello 磁碟區容量。
* **型別**– 指出 hello 磁碟區是否為**分層**(hello 預設) 或**固定在本機**。
* **備份**– 指出 hello 磁碟區是否有預設的備份原則存在。
* **存取**– 指定允許存取 toothis 磁碟區的 hello 啟動器 （伺服器）。 不是成員的存取控制記錄 (ACR) 與 hello 磁碟區相關聯的啟動器不會看到 hello 磁碟區。
* **監視** – 指定是否正在監視磁碟區。 預設會在建立磁碟區時啟用監視。 不過，磁碟區複製會停用監視。 tooenable 監視磁碟區，請依照下列中的 hello 指示[監視磁碟區](#monitor-a-volume)。 

使用 hello 指示在本教學課程 tooperform hello，下列工作：

* 新增磁碟區 
* 修改磁碟區 
* 變更 hello 磁碟區類型
* 刪除磁碟區 
* 使磁碟區離線 
* 監視磁碟區 

## <a name="add-a-volume"></a>新增磁碟區
您已在部署 StorSimple 方案期間 [建立磁碟區](storsimple-deployment-walkthrough-u2.md#step-6-create-a-volume) 。 新增磁碟區會是類似的程序。

#### <a name="tooadd-a-volume"></a>tooadd 磁碟區
1. 在 [hello**裝置**頁面、 選取 hello 裝置、 按兩下，然後再按一下 hello**磁碟區容器**] 索引標籤。
2. 從 hello 清單中選取磁碟區容器，然後按兩下該 tooaccess hello 與 hello 容器相關聯的磁碟區。
3. 按一下**新增**hello hello 頁底端。 hello 新增磁碟區精靈 會啟動。
   
     ![加入磁碟區精靈基本設定](./media/storsimple-manage-volumes-u2/TieredVolEx.png)
4. 在 [hello 新增磁碟區精靈] 中，在**基本設定**，不要遵循 hello:
   
   1. 輸入磁碟區的 [名稱]  。
   2. 選取**使用類型**hello 下拉式清單中。 針對需要時時保有資料 toobe hello 裝置本機上可用的工作負載，請選取**固定在本機**。 對於所有其他資料類型，選取 [分層]。 (**分層**hello 預設值。)
   3. 如果您選取**分層**在步驟 2 中，您可以選取 hello**對於不常存取的封存資料，使用此磁碟區**核取方塊 tooconfigure 封存的磁碟區。
   4. 輸入 hello**佈建的容量**以 GB 或 TB 磁碟區。 請參閱 [佈建的容量](#provisioned-capacity) 以取得每個裝置與磁碟區類型的最大大小。 查看 hello**可用容量**toodetermine 多少儲存空間是您的裝置上的實際可用。
5. 按一下 [hello] 箭號圖示![箭號圖示](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png). 如果您要設定本機固定磁碟區，您會看到下列訊息的 hello。
   
    ![變更磁碟區類型訊息](./media/storsimple-manage-volumes-u2/LocalVolEx.png)
6. 按一下 [hello] 箭號圖示![箭號圖示](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png)再次 toogo toohello**其他設定**頁面。
   
    ![加入磁碟區精靈其他設定](./media/storsimple-manage-volumes-u2/AddVolume2.png)<br>
7. 在 [其他設定] 下，加入新的存取控制記錄 (ACR)：
   
   1. 從 hello 下拉式清單中選取存取控制記錄 (ACR)。 或者，您可以加入新的 ACR。 Acr 可讓您判斷哪些主機可以存取您的磁碟區比對的 hello 使用 hello 記錄中列出的主機 IQN。 如果您沒有指定 ACR，您會看到下列訊息的 hello。
      
        ![指定 ACR](./media/storsimple-manage-volumes-u2/SpecifyACR.png)
   2. 我們建議您選取 hello**啟用此磁碟區的預設備份**核取方塊。
   3. 按一下 [hello] 核取圖示 ![核取圖示](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png) 以 hello toocreate hello 磁碟區指定的設定。

您新的磁碟區現在已準備好 toouse。

> [!NOTE]
> 如果您建立本機固定磁碟區，然後再建立另一部本機固定磁碟區，立即 hello 磁碟區建立工作之後，以循序方式執行。 hello 第一個磁碟區建立作業必須完成才能開始進行 hello 下一個磁碟區建立工作。
> 
> 

## <a name="modify-a-volume"></a>修改磁碟區
當您需要 tooexpand 它或變更 hello 存取 hello 的磁碟區的主機時，請修改磁碟區。

> [!IMPORTANT]
> * 如果您修改 hello hello 裝置上的磁碟區大小，hello 磁碟區大小需要 toobe hello 主控件上的變更。 
> * 此處所述的 hello 主機端步驟適用於 Windows Server 2012 (2012R2)。 Linux 或其他主機作業系統的程序會有所不同。 修改 hello 執行另一個作業系統的主機上的磁碟區時，請參閱 tooyour 主機作業系統的指示。 
> 
> 

#### <a name="toomodify-a-volume"></a>toomodify 磁碟區
1. 在 [hello**裝置**頁面、 選取 hello 裝置、 按兩下，然後再按一下 hello**磁碟區容器**] 索引標籤。
2. 從 hello 清單中選取磁碟區容器，然後按兩下該 tooview hello 磁碟區與 hello 容器相關聯。
3. 選取磁碟區，然後在 hello hello 頁面底部，按一下 **修改**。 hello 修改磁碟區精靈 隨即啟動。
4. 在 hello 修改磁碟區精靈 在**基本設定**，您可以 hello 下列：
   
   * 編輯 hello**名稱**。
   * 轉換 hello**使用類型**從本機固定 tootiered 或釘選的分層式 toolocally (請參閱[變更 hello 磁碟區類型](#change-the-volume-type)如需詳細資訊)。
   * 增加 hello**佈建的容量**。 hello**佈建的容量**只能增加。 您無法在磁碟區建立後予以壓縮。
5. 在下**其他設定**，您可以修改 hello ACR，前提是 hello 磁碟區已離線。 Hello 磁碟區已上線時，如果您需要 tootake 它離線的第一個。 Toohello 中的步驟，請參閱[使磁碟區離線](#take-a-volume-offline)先前 toomodifying hello ACR。
   
   > [!NOTE]
   > 您無法變更 hello**啟用預設備份**hello 磁碟區的選項。
   > 
   > 
6. 按一下 hello 核取圖示以儲存您的變更 ![核取圖示](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png). hello Azure 傳統入口網站將會顯示更新的磁碟區訊息。 已成功更新 hello 磁碟區時，它會顯示成功訊息。
7. 如果您要擴充磁碟區，完成下列步驟在您的 Windows 主機電腦上的 hello:
   
   1. 跳過**電腦管理** ->**磁碟管理**。
   2. 以滑鼠右鍵按一下 [磁碟管理]，並選取 [重新掃描磁碟]。
   3. 在 hello 清單中的磁碟，選取您更新的 hello 磁碟區、 按一下滑鼠右鍵，然後選取**延伸磁碟區**。 hello 延伸磁碟區精靈 隨即啟動。 按一下 [下一步] 。
   4. 完成 hello 精靈，接受 hello 的預設值。 Hello 精靈完成後，hello 磁碟區應該會顯示 hello 增加大小。
      
      > [!NOTE]
      > 如果您展開本機固定磁碟區，然後展開本機另一個 hello 磁碟區延伸作業之後，以循序方式執行，請立即固定磁碟區。 hello 第一個磁碟區擴充工作必須完成才能開始進行下一個磁碟區擴充工作 hello。
      > 
      > 

![提供的影片](./media/storsimple-manage-volumes-u2/Video_icon.png) **提供的影片**

toowatch 的視訊示範，如何 tooexpand 磁碟區，按一下[這裡](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/)。

## <a name="change-hello-volume-type"></a>變更 hello 磁碟區類型
您可以變更 hello 磁碟區類型從分層式 toolocally 釘選，或從本機固定 tootiered。 不過，這種轉換不應該經常發生。 某些階層式 toolocally 釘選的轉換磁碟區的原因如下：

* 關於資料可用性和效能的本機保證
* 消除雲端延遲和雲端連線問題。

一般來說，這些是小型經常想 tooaccess 的現有磁碟區。 當固定在本機的磁碟區建立時，它就會完整佈建。 如果您想要轉換的階層式磁碟區 tooa 固定在本機磁碟區，StorSimple 會確認您在裝置上有足夠的空間，開始 hello 轉換之前。 如果您有足夠的空間，您會收到錯誤，且會取消 hello 作業。 

> [!NOTE]
> 開始從釘選的分層式 toolocally 轉換之前，請確定您考慮 hello 空間需求的其他工作負載。 
> 
> 

您可能想 toochange 本機固定磁碟區 tooa 分層磁碟區如果您需要額外的空間 tooprovision 其他磁碟區。 當您轉換 hello 固定在本機磁碟區 tootiered 時，hello hello 釋出容量大小會增加 hello hello 裝置上的可用容量。 如果連線問題會使磁碟區的 hello 轉換從 hello 區域型別 toohello 層型別，hello 本機磁碟區會展示分層磁碟區的內容之前 hello 轉換完成。 這是因為某些資料可能會溢出 toohello 雲端。 此餘力的資料會繼續 toooccupy hello 作業會重新啟動時，完成之前無法釋放的 hello 裝置上的本機空間。

> [!NOTE]
> 轉換磁碟區可能需要一些時間，且您在啟動之後無法取消轉換。 hello 磁碟區仍在進行 hello 轉換時，線上和才能進行備份，但您無法展開或 hello 轉換正在進行時，還原 hello 磁碟區。  
> 
> 

從階層式的 tooa 固定在本機磁碟區的轉換可能會影響裝置的效能。 此外，hello 下列因素可能會增加 hello toocomplete hello 轉換所花費的時間：

* 頻寬不足。
* 沒有最新備份。

這些因素可能會有的 toominimize hello 效果：

* 請檢閱頻寬節流設定原則，並確認有專用的 40 Mbps 頻寬。
* 排程離峰時間的 hello 轉換。
* 在開始 hello 轉換之前，請建立的雲端快照。

如果您想要轉換多個磁碟區 （支援不同的工作負載），您應該設定 hello 磁碟區轉換優先權，優先權較高的磁碟區會先轉換。 例如，您應該先轉換裝載虛擬機器 (VM) 的磁碟區，或具有 SQL 工作負載的磁碟區，然後才轉換檔案共用工作負載的磁碟區。

#### <a name="toochange-hello-volume-type"></a>toochange hello 磁碟區類型
1. 在 [hello**裝置**頁面、 選取 hello 裝置、 按兩下，然後再按一下 hello**磁碟區容器**] 索引標籤。
2. 從 hello 清單中選取磁碟區容器，然後按兩下該 tooview hello 磁碟區與 hello 容器相關聯。
3. 選取磁碟區，然後在 hello hello 頁面底部，按一下 **修改**。 hello 修改磁碟區精靈 隨即啟動。
4. 在 hello**基本設定**頁面上，從 hello 選取 hello 新類型來變更 hello 使用類型**使用類型**下拉式清單。
   
   * 如果您要變更 hello 類型太**固定在本機**，StorSimple 會檢查 toosee，如果沒有足夠的容量。
   * 如果您要變更 hello 類型太**分層**及此磁碟區會用於封存資料，選取 hello**對於不常存取的封存資料，使用此磁碟區**核取方塊。
     
       ![封存核取方塊](./media/storsimple-manage-volumes-u2/ModifyTieredVolEx.png)
5. 按一下 [hello] 箭號圖示![箭號圖示](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png)toogo toohello**其他設定**頁面。 如果您要設定本機固定磁碟區，hello 會出現下列訊息。
   
    ![變更磁碟區類型訊息](./media/storsimple-manage-volumes-u2/ModifyLocalVolEx.png)
6. 按一下 [hello] 箭號圖示 ![箭號圖示](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png) 再次 toocontinue。
7. 按一下 [hello] 核取圖示 ![核取圖示](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png) toostart hello 轉換程序。 hello Azure 入口網站將會顯示更新的磁碟區訊息。 已成功更新 hello 磁碟區時，它會顯示成功訊息。

## <a name="take-a-volume-offline"></a>使磁碟區離線
您可能需要 tootake 磁碟區離線，當您計劃 toomodify 它或刪除它。 當磁碟區離線時，即無法進行讀寫存取。 您將需要 tootake hello 磁碟區離線 hello 裝置以及 hello 主機上。 

#### <a name="tootake-a-volume-offline"></a>tootake 磁碟區離線
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

#### <a name="toodelete-a-volume"></a>toodelete 磁碟區
1. 在 [hello**裝置**頁面、 選取 hello 裝置、 按兩下，然後再按一下 hello**磁碟區容器**] 索引標籤。
2. 選取您想要 toodelete hello 磁碟區的 hello 磁碟區容器。 按一下 hello 磁碟區容器 tooaccess hello**磁碟區**頁面。
3. 與這個容器相關聯的所有 hello 磁碟區會以表格格式都顯示。 檢查 hello 狀態想 toodelete hello 磁碟區。 如果您想要 toodelete hello 磁碟區未離線，使其離線的第一個步驟，下列 hello 步驟[使磁碟區離線](#take-a-volume-offline)。
4. Hello 磁碟區離線後，請按一下**刪除**hello hello 頁底端。
5. 系統提示您進行確認時，按一下 [是] 。 hello 磁碟區現在將會刪除與 hello**磁碟區**頁面會顯示更新的 hello hello 容器內的磁碟區清單。
   
   > [!NOTE]
   > 如果您刪除本機固定磁碟區，可能不會立即更新 hello 空間供新磁碟區。 hello StorSimple Manager 服務會定期更新 hello 可用的本機空間。 我們建議您等待幾分鐘的時間再 toocreate hello 新磁碟區。<br> 此外，如果您刪除本機固定磁碟區，然後再刪除另一部本機固定磁碟區，立即 hello 大量刪除作業之後，以循序方式執行。 hello 第一個磁碟區刪除工作必須完成才能開始進行下一個磁碟區刪除工作 hello。
   > 
   > 

## <a name="monitor-a-volume"></a>監視磁碟區
磁碟區監視可讓您的磁碟區的 toocollect 我 I/O 相關統計資料。 預設值為 hello 會啟用監視您所建立的前 32 磁碟區。 預設會停用監視其他磁碟區。 預設也會停用監視複製的磁碟區。

執行下列步驟 tooenable hello 或停用磁碟區的監視。

#### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable 或停用磁碟區監視
1. 在 [hello**裝置**頁面、 選取 hello 裝置、 按兩下，然後再按一下 hello**磁碟區容器**] 索引標籤。
2. 選取哪些 hello 磁碟區所在，hello 磁碟區容器，然後按一下hello 磁碟區容器 tooaccess hello**磁碟區**頁面。
3. 與這個容器相關聯的所有 hello 磁碟區會都列在 hello 表格式顯示中。 按一下並選取 hello 磁碟區或磁碟區再製。
4. 在 hello hello 頁面底部，按一下**修改**。
5. 在 hello 修改磁碟區精靈 在**基本設定**，選取**啟用**或**停用**從 hello**監視**下拉式清單。

## <a name="next-steps"></a>後續步驟
* 了解如何太[複製 StorSimple 磁碟區](storsimple-clone-volume.md)。
* 了解如何太[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。

