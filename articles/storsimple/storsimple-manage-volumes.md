---
title: "管理 StorSimple 磁碟區 | Microsoft Docs"
description: "說明如何加入、修改及監視 StorSimple 磁碟區，以及如何在必要時使其離線。"
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
ms.openlocfilehash: 31ed9dad8ba56a3746873b7b35e678e97743fbfe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-volumes"></a>使用 StorSimple Manager 服務來管理磁碟區
[!INCLUDE [storsimple-version-selector-manage-volumes](../../includes/storsimple-version-selector-manage-volumes.md)]

## <a name="overview"></a>概觀
本教學課程說明如何使用 StorSimple Manager 服務來建立和管理 StorSimple 裝置與 StorSimple 虛擬裝置上的磁碟區。

StorSimple Manager 服務是 Azure 傳統入口網站的延伸模組，可讓您透過單一 Web 介面管理 StorSimple 解決方案。 除了管理磁碟區，您可以使用 StorSimple Manager 服務來建立和管理 StorSimple 服務、檢視和管理裝置、檢視警示，以及檢視和管理備份原則與備份類別目錄。

> [!NOTE]
> Azure StorSimple 只能建立精簡佈建的磁碟區。 您無法在 Azure StorSimple 系統上建立完整佈建或部分佈建的磁碟區。
> 
> 精簡佈建是一項虛擬化技術，讓可用的儲存空間超過實體資源。 Azure StorSimple 不預先保留足夠的儲存空間，而是利用精簡佈建來配置剛好符合目前需求的空間。 雲端儲存體本質有彈性可協助這種方法，因為 Azure StorSimple 可以隨需求變化，增加或減少雲端儲存體。
> 
> 

## <a name="the-volumes-page"></a>[磁碟區] 頁面
您為啟動器 (伺服器) 佈建在 Microsoft Azure StorSimple 裝置的存放磁碟區，可以在 [磁碟區]  頁面管理 。 它會顯示 StorSimple 裝置上的磁碟區清單。

 ![磁碟區頁面](./media/storsimple-manage-volumes/HCS_VolumesPage.png)

磁碟區是由一系列屬性所組成：

* **名稱** – 必須是唯一且有助於識別磁碟區的描述性名稱。 這個名稱也可在您篩選特定磁碟區時用於監視報告。
* **狀態** – 可為連線或離線。 如果是離線的磁碟區，允許存取使用它的啟動器 (伺服器) 會看不到該磁碟區。
* **容量** – 指定啟動器 (伺服器) 所認知的磁碟區大小。 容量指定啟動器 (伺服器) 可以儲存的總資料量。 磁碟區採精簡佈建，而且會刪除重複的資料。 這表示您的裝置不會根據設定的磁碟區容量，在內部或在雲端預先配置實體儲存體容量。 磁碟區容量會依需求來配置和耗用。
* **類型** – 磁碟區類型可以是分層或封存 (子類型分層)
* **存取** – 指定允許存取此磁碟區的啟動器 (伺服器)。 啟動器不是與磁碟區相關聯的存取控制記錄 (ACR) 成員，就看不到磁碟區。
* **監視** – 指定是否正在監視磁碟區。 預設會在建立磁碟區時啟用監視。 不過，磁碟區複製會停用監視。 若要啟用監視磁碟區，請依照＜監視磁碟區＞中的指示執行。

最常見與磁碟區相關聯的工作如下：

* 新增磁碟區
* 修改磁碟區
* 刪除磁碟區
* 使磁碟區離線
* 監視磁碟區

## <a name="add-a-volume"></a>新增磁碟區
您已在部署 StorSimple 方案期間 [建立磁碟區](storsimple-deployment-walkthrough-u1.md#step-6-create-a-volume) 。 新增磁碟區會是類似的程序。

### <a name="to-add-a-volume"></a>若要新增磁碟區
1. 在 [裝置] 頁面中，選取並按兩下裝置，然後按一下 [磁碟區容器] 索引標籤。
2. 選取磁碟區容器，然後按一下對應資料列的箭號來存取與該容器相關聯的磁碟區。
3. 按一下頁面底部的 [新增]  。 [新增磁碟區精靈] 隨即啟動。
   
     ![加入磁碟區精靈基本設定](./media/storsimple-manage-volumes/AddVolume1.png)
4. 在 [新增磁碟區精靈] 的 [基本設定] 下，執行列動作：
   
   1. 輸入磁碟區的 [名稱]  。
   2. 為磁碟區指定 [佈建的容量]  \(GB 或 TB)。 實體裝置的容量必須介於 1 GB 到 64 TB 之間。 可為 StorSimple 虛擬裝置上的磁碟區佈建的最大容量為 30 TB。
   3. 為磁碟區選取 [使用類型]  。 如果您針對封存資料使用分層磁碟區，選取 [使用此磁碟區存放不常存取的封存資料]  核取方塊會將您磁碟區的重複資料刪除區塊大小變更為 512 KB。 如果未核取此選項，對應的分層磁碟區會使用 64 KB 的區塊大小。 較大的重複資料刪除區塊大小可讓裝置加速傳送大型封存資料到雲端 (分層式磁碟區之前稱為主要磁碟區)。
   4. 按一下箭頭圖示![箭頭圖示](./media/storsimple-manage-volumes/HCS_ArrowIcon.png)，前往 [其他設定] 頁面。
      
        ![加入磁碟區精靈其他設定](./media/storsimple-manage-volumes/AddVolume2.png)
5. 在 [其他設定] 下，加入新的存取控制記錄 (ACR)：
   
   1. 在下拉式清單中選取存取控制記錄 (ACR)。 或者，您可以加入新的 ACR。 ACR 會藉由比對主機與記錄中列出的 IQN 來決定哪些主機可以存取磁碟區。
   2. 建議選取 [ **啟用此磁碟區的預設備份** ] 核取方塊啟用預設備份。
   3. 按一下核取圖示  ![核取圖示](./media/storsimple-manage-volumes/HCS_CheckIcon.png) ，以利用指定的設定來建立磁碟區。

新的磁碟區現在已備妥可供使用。

## <a name="modify-a-volume"></a>修改磁碟區
當您需要擴充磁碟區，或變更存取該磁碟區的主機時，請修改磁碟區。

> [!IMPORTANT]
> * 如果您修改裝置上的磁碟區大小，也必須變更主機上的磁碟區大小。
> * 此處所述的主機端步驟適用於 Windows Server 2012 (2012R2)。 Linux 或其他主機作業系統的程序會有所不同。 如果要在執行其他作業系統的主機上修改磁碟區，請參考主機作業系統的指示。
> 
> 

### <a name="to-modify-a-volume"></a>若要修改磁碟區
1. 在 [裝置] 頁面中，選取並按兩下裝置，然後按一下 [磁碟區容器] 索引標籤。 此頁面會以表格列出與裝置相關聯的所有磁碟區容器。
2. 選取並按一下磁碟區容器，以清單顯示該容器內的所有磁碟區。
3. 在 [磁碟區] 頁面上，選取磁碟區，然後按一下 [修改]。
4. 在 [修改磁碟區精靈] 的 [基本設定] 下，您可以執行列動作：
   
   * 如果您要藉由選取 [使用此磁碟區存放不常存取的封存資料] 核取方塊，將您磁碟區的重複資料刪除區塊大小變更為 512 KB，將分層磁碟區修改為封存磁碟區，請編輯 [名稱] 和 [類型]。
   * 增加 [佈建的容量] 。 [佈建的容量]  只能增加。 您無法在磁碟區建立後予以壓縮。
     
     > [!NOTE]
     > 磁碟區容器一經指派給磁碟區後，便無法變更。
     > 
     > 
5. 在 [其他設定] 下，您可以執行下列動作：
   
   * 修改 ACR，若是磁碟區已離線。 如果磁碟區已連線，您必須先讓它離線。 修改 ACR 之前，請參閱 [使磁碟區離線](#take-a-volume-offline) 中的步驟。
   * 在磁碟區離線之後，才修改 ACR 清單。
     
     > [!NOTE]
     > 您無法變更此磁碟區的 [ **啟用此磁碟區的預設備份** ] 選項。
     > 
     > 
6. 按一下核取圖示  ![核取圖示](./media/storsimple-manage-volumes/HCS_CheckIcon.png)。 Azure 傳統入口網站將會顯示更新磁碟區訊息。 如果磁碟區已成功更新，即會顯示成功訊息。
7. 如果您要延伸磁碟區，請在 Windows 主機電腦上完成下列步驟：
   
   1. 移至 [電腦管理]  ->[磁碟管理]。
   2. 以滑鼠右鍵按一下 [磁碟管理]，並選取 [重新掃描磁碟]。
   3. 在磁碟清單中，選取您已更新的磁碟區，按一下滑鼠右鍵，然後選取 [延伸磁碟區] 。 [延伸磁碟區精靈] 隨即啟動。 按一下 [下一步] 。
   4. 使用預設值完成精靈。 完成精靈後，磁碟區應該會顯示增加的大小。

![提供的影片](./media/storsimple-manage-volumes/Video_icon.png) **提供的影片**

若要觀看影片示範如何擴充磁碟區，請按一下 [這裡](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/)。

## <a name="take-a-volume-offline"></a>使磁碟區離線
您想要修改或刪除磁碟區時，可能需要先使其離線。 當磁碟區離線時，即無法進行讀寫存取。 您必須使主機與裝置上的磁碟區同時離線。 請執行下列步驟以使磁碟區離線。

### <a name="to-take-a-volume-offline"></a>若要使磁碟區離線
1. 請確定有問題的磁碟區不在使用中後，再使其離線。
2. 先使主機上的磁碟區離線。 這樣做可以排除任何會造成磁碟區上資料損毀的潛在風險。 如需特定步驟，請參閱主機作業系統的指示。
3. 在主機離線之後，請執行下列步驟以使裝置上的磁碟區離線：
   
   1. 在 [裝置] 頁面中，選取並按兩下裝置，然後按一下 [磁碟區容器] 索引標籤。 [磁碟區容器]  索引標籤會以表格列出與裝置相關聯的所有磁碟區容器。
   2. 選取並按一下磁碟區容器，以清單顯示該容器內的所有磁碟區。
   3. 選取磁碟區，然後按一下 [離線] 。
   4. 系統提示您進行確認時，按一下 [是] 。 磁碟區現在應已離線。
      
      磁碟區離線之後，[上線]  選項就會變成可用。

> [!NOTE]
> [離線] 命令會將要求傳送到裝置，以使磁碟區離線。 如果主機仍在使用該磁碟區，這會導致連線中斷，但是使磁碟區離線不會失敗。
> 
> 

## <a name="delete-a-volume"></a>刪除磁碟區
> [!IMPORTANT]
> 只有當磁碟區離線時，您才能予以刪除。
> 
> 

請完成下列步驟來刪除磁碟區。

### <a name="to-delete-a-volume"></a>若要刪除磁碟區
1. 在 [裝置] 頁面中，選取並按兩下裝置，然後按一下 [磁碟區容器] 索引標籤。
2. 選取含有您想要刪除之磁碟區的磁碟區容器。 按一下該磁碟區容器，即可存取 [磁碟區]  頁面。
3. 與這個容器相關聯的所有磁碟區會以表格顯示。 檢查您想要刪除之磁碟區的狀態。 如果您想要刪除的磁碟區未離線，請先使其離線，請依照 [使磁碟區離線](#take-a-volume-offline)中的步驟執行。
4. 在磁碟區離線之後，按一下頁面底部的 [刪除]  。
5. 系統提示您進行確認時，按一下 [是] 。 現已刪除磁碟區，而 [磁碟區]  頁面會顯示容器內已更新的磁碟區清單。

## <a name="monitor-a-volume"></a>監視磁碟區
監視磁碟區可讓您為磁碟區收集 I/O 相關的統計資料。 根據預設，您建立的前 32 個磁碟區會啟用監視。 預設會停用監視其他磁碟區。 預設也會停用監視複製的磁碟區。

請執行下列步驟來啟用或停用監視磁碟區。

### <a name="to-enable-or-disable-volume-monitoring"></a>若要啟用或停用監視磁碟區
1. 在 [裝置] 頁面中，選取並按兩下裝置，然後按一下 [磁碟區容器] 索引標籤。
2. 選取磁碟區所在的磁碟區容器，然後按一下該磁碟區容器來存取 [磁碟區]  頁面。
3. 以表格顯示所列出與這個容器相關聯的所有磁碟區。 按一下並選取磁碟區或磁碟區複製。
4. 按一下頁面底部的 [修改] 。
5. 在 [修改磁碟區精靈] 的 [基本設定] 下，從 [監視] 下拉式清單中選取 [啟用] 或 [停用]。
   
    ![修改磁碟區基本設定](./media/storsimple-manage-volumes/HCS_MonitorVolumeM.png)

## <a name="next-steps"></a>後續步驟
* 了解如何 [複製 StorSimple 磁碟區](storsimple-clone-volume.md)。
* 了解如何 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。

