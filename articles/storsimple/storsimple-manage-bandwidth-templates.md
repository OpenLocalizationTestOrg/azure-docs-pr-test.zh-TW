---
title: "aaaManage StorSimple 頻寬範本 |Microsoft 文件"
description: "描述如何 toomanage StorSimple 頻寬範本，可讓您 toocontrol 頻寬耗用量。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 0027b90e-91a5-437d-9bd0-06b05674aa5f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2016
ms.author: alkohli
ms.openlocfilehash: 3f767e985667121e977106e7a1f8e5a3ad25f022
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-storsimple-bandwidth-templates"></a>使用 hello StorSimple Manager 服務 toomanage StorSimple 頻寬範本
## <a name="overview"></a>概觀
頻寬範本可讓您 tooconfigure 網路頻寬使用跨多個日期時間排程 tootier hello 資料從 hello StorSimple 裝置 toohello 雲端。

利用頻寬節流排程，您可以：

* 指定自訂的頻寬排程視 hello 工作負載的網路使用方式而定。
* 集中管理，並重複跨多個裝置的 hello 排程使用簡便而順暢的方式。

> [!NOTE]
> 這項功能只可供 StorSimple 實體裝置使用，不能用於虛擬裝置。
> 
> 

所有的 hello 頻寬範本，為您的服務會顯示在以表格式，並包含下列資訊的 hello:

* **名稱**– 指派唯一名稱 toohello 頻寬範本建立時。
* **排程**– hello 給定的頻寬範本中包含的排程數目。
* **使用**– hello 使用 hello 頻寬範本的磁碟區數目。

使用 hello StorSimple Manager 服務**設定**hello Azure 傳統入口網站 toomanage 頻寬範本中的頁面。

您也可以找到其他資訊 toohelp 設定頻寬範本中：

* 頻寬範本的相關問與答
* 頻寬範本的最佳作法

## <a name="add-a-bandwidth-template"></a>新增頻寬範本
執行下列步驟 toocreate 新的頻寬範本的 hello。

#### <a name="tooadd-a-bandwidth-template"></a>tooadd 頻寬範本
1. 在 hello StorSimple Manager 服務**設定**頁面上，按一下**新增/編輯頻寬範本**。
2. 在 hello**新增/編輯頻寬範本**對話方塊：
   
   1. 從 hello**範本**下拉式清單中，選取**建立新**tooadd 新的頻寬範本。
   2. 為頻寬範本指定唯一的名稱。
3. 定義 **頻寬排程**。 toocreate 排程：
   
   1. 從 hello 下拉式清單中，選擇設定 hello hello 週 hello 排程的天數。 您可以選取多天 hello hello 清單中的 hello 各日期前面的核取方塊。
   2. 選取 hello**全天**hello 排程是否僅限於 hello 整天選項。 核取此選項時，您無法再指定 [開始時間] 或 [結束時間]。 hello 排程執行從 12:00 AM too11: 59 PM。
   3. 從 hello 下拉式清單中，選取 **開始時間**。 這是當 hello 排程就會開始。
   4. 從 hello 下拉式清單中，選取 **結束時間**。 這是 hello 排程將會停止。
      
      > [!NOTE]
      > 不允許重疊的排程。 如果 hello 開始和結束時間會產生重疊的排程，您會看到錯誤訊息 toothat 效果。
      > 
      > 
   5. 指定 hello**頻寬速率**。 這是以 mb / 秒 (Mbps 牽涉 hello 雲端 （上傳和下載） 的作業在 StorSimple 裝置所使用) 的 hello 頻寬。 提供一個介於 1 到 1000 之間的數目給此欄位。
   6. 按一下核取圖示，hello![核取圖示](./media/storsimple-manage-bandwidth-templates/HCS_CheckIcon.png)。 您已建立的 hello 範本將會新增頻寬範本清單 toohello hello 服務上**設定**頁面。
      
      ![建立新的頻寬範本](./media/storsimple-manage-bandwidth-templates/HCS_CreateNewBT1.png)
4. 按一下**儲存**在 hello hello 頁面，然後按一下底部**是**出現確認提示時。 這樣會儲存您所做的 hello 組態變更。

## <a name="edit-a-bandwidth-template"></a>編輯頻寬範本
執行下列步驟 tooedit 頻寬範本的 hello。

### <a name="tooedit-a-bandwidth-template"></a>tooedit 頻寬範本
1. 按一下 [ **新增/編輯頻寬範本**]。
2. 在 hello**新增/編輯頻寬範本**對話方塊：
   
   1. 從 hello**範本**下拉式清單中，選擇現有的頻寬範本的 toomodify。
   2. 完成您的變更。 （您可以修改任何 hello 現有設定。）
   3. 按一下 [hello] 核取圖示 ![核取圖示](./media/storsimple-manage-bandwidth-templates/HCS_CheckIcon.png). Hello 服務設定 頁面上，您會看到在 hello 頻寬範本清單中的 hello 已修改的範本。
3. 您的變更，按一下 toosave**儲存**hello hello 頁底端。 在頁面底部按一下 [ **是** ]。

> [!NOTE]
> 您不會允許您的變更，如果與現有的 hello 已編輯的排程重疊排程 hello 頻寬範本中您要修改的 toosave。
> 
> 

## <a name="delete-a-bandwidth-template"></a>刪除頻寬範本
執行下列步驟 toodelete 頻寬範本的 hello。

#### <a name="toodelete-a-bandwidth-template"></a>toodelete 頻寬範本
1. 在您的服務的 hello 頻寬範本表格式清單中 hello，選取您想 toodelete hello 範本。 刪除圖示 (**x**) 會出現 toohello 最右側的 hello 選取的範本。 按一下 hello **x**圖示 toodelete hello 範本。
2. 系統將提示您進行確認。 按一下**確定**tooproceed。

如果任何磁碟區的使用中 hello 範本，您不能 toodelete 它。 您會看到錯誤訊息，指出正在使用該 hello 範本。 錯誤訊息對話方塊會通知您，應該移除所有 hello 參考 toohello 範本。

您可以藉由存取 hello 刪除所有的 hello 參考 toohello 範本**磁碟區容器**頁面上，並修改使用此範本，讓它們使用另一個範本，或使用自訂或無限制頻寬的 hello 磁碟區容器設定。 當所有 hello 參考已都移除之後時，您可以刪除 hello 範本。

## <a name="use-a-default-bandwidth-template"></a>使用預設頻寬範本
預設頻寬範本提供，並可供磁碟區容器依預設 tooenforce 頻寬控制存取 hello 雲端。 hello 預設範本也可做為現成的參考的使用者建立其自己的範本。 此預設範本的 hello 詳細資料如下：

* **名稱** – 不限制夜間和週末
* **排程**– 從星期一 tooFriday 適用於上午 8 點和下午 5 點裝置時間之間的 1 Mbps 的頻寬速率的單一排程。 hello 頻寬設定 tooUnlimited hello 週 hello 其餘部分。

可以編輯 hello 預設範本。 hello 使用量 （包括已編輯的版本） 這個範本會追蹤。

## <a name="create-an-all-day-bandwidth-template-that-starts-at-a-specified-time"></a>建立在指定時間啟動的全天頻寬範本
請遵循此程序 toocreate 在指定時間啟動並執行所有日期的排程。 在 hello 範例中，hello 排程 hello 早上 9 點開始，直到上午 9 點 hello 隔天早上執行。 很重要的 toonote hello 開始，並指定排程的結束時間都必須包含在 hello 相同 24 小時排程，且不能跨越多天。 如果您需要 tooset 向上跨多天的頻寬範本，您將需要 toouse 多個排程 （如 hello 範例所示）。

#### <a name="toocreate-an-all-day-bandwidth-template"></a>toocreate 全天頻寬範本
1. 建立在 hello 早上 9 點啟動並執行到午夜的排程。
2. 新增另一個排程。 設定從午夜 hello 第二個排程 toorun hello 早上 9 點。
3. 儲存 hello 頻寬範本。

接著在您選擇的時間啟動並全天執行 hello 複合排程。

## <a name="questions-and-answers-about-bandwidth-templates"></a>頻寬範本的相關問與答
**問：** 發生什麼事 toobandwidth 控制項 hello 排程之間會？ (一個排程已結束而另一個排程尚未開始)。

**答：** 在這種情況下，不會採用任何頻寬控制。 這表示該 hello 裝置分層資料 toohello 雲端時，可以使用無限制的頻寬。

**問：** 您是否可以修改離線裝置上的頻寬範本？

**答：** 如果 hello 對應的裝置已離線，您將無法能 toomodify 磁碟區容器上的頻寬範本。

**問：** 您可以編輯 hello 相關聯的磁碟區離線時，與磁碟區容器相關聯的頻寬範本嗎？

**答：** 您可以修改和磁碟區已離線之磁碟區容器相關聯的頻寬範本。 請注意，當磁碟區離線，任何資料會分層從 hello 裝置 toohello 雲端。

**問：** 您是否可以刪除預設範本？

**答：** 雖然您可以刪除預設範本，但它並不建議 toodo。 hello 使用量的預設範本，包括已編輯的版本中，系統會追蹤。 hello 追蹤資料分析，並透過 hello 課程中的時間，是使用的 tooimprove hello 預設範本。

**問：** 如何判斷頻寬範本需要 toobe 修改？

**答：** 一開始時，您需要 toomodify hello 頻寬範本的徵兆的 hello 看見 hello 網路變慢或在一天多次阻礙。 如果發生這種情況，請查看 hello I/O 效能及網路輸送量圖表監視 hello 儲存體和使用網路。

從 hello 網路輸送量資料中，找出 hello 一天的時間並 hello 中的 hello 網路瓶頸後，就會發生的磁碟區容器。 如果發生這種情況時資料分層式的 toohello 雲端 （取得這項資訊的所有磁碟區容器從 I/O 效能裝置 toocloud），則需要 toomodify hello 頻寬範本與磁碟區容器相關聯。

Hello 修改後範本正在使用中，您必須 toomonitor hello 網路一次無顯著的延遲。 如果這些狀況仍存在，則您需要 toorevisit 頻寬範本。

**問：** 萬一我的裝置上的多個磁碟區容器有重疊的排程，但不同限制套用 tooeach 嗎？

**答：** 假設您的裝置有 3 個磁碟區容器。 hello 完全與這些容器相關聯的排程重疊。 針對每個容器，使用 hello 頻寬限制分別 5、 10 和 15 Mbps。 當 I/o 所發生的所有可能套用相同的時間，hello 最小值為 hello 3 頻寬限制的 hello 在這些容器： 在此情況下，因此這些傳出 I/O 要求共用為 5 Mbps hello 相同的佇列。

## <a name="best-practices-for-bandwidth-templates"></a>頻寬範本的最佳作法
請遵循 StorSimple 裝置的最佳作法：

* 設定您裝置 tooenable 變數節流的 hello 網路輸送量 hello 裝置在 hello 每天不同時間的頻寬範本。 這些頻寬範本和備份排程搭配使用時，可以在離峰時段期間有效利用雲端作業的其他網路頻寬。
* 計算所需的基礎 hello 大小 hello 部署與 hello 所需的復原時間目標 (RTO) 的特定部署的 hello 實際頻寬。

## <a name="next-steps"></a>後續步驟
深入了解[使用您的 StorSimple 裝置 hello StorSimple Manager 服務 tooadminister](storsimple-manager-service-administration.md)。

