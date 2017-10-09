---
title: "aaaClone StorSimple Virtual Array 備份 |Microsoft 文件"
description: "深入了解如何 tooclone 備份和復原的檔案從您的 StorSimple Virtual Array。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: af6e979c-55e3-477c-b53e-a76a697f80c9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: 21bfcae48ee07762179cf00ce842b6094abe18ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="clone-from-a-backup-of-your-storsimple-virtual-array"></a>從 StorSimple Virtual Array 的備份複製

## <a name="overview"></a>概觀

本文逐步如何 tooclone 備份您的共用或磁碟區上設定您 Microsoft Azure StorSimple Virtual Array。 hello 複製的備份是使用的 toorecover 已刪除或遺失的檔案。 hello 發行項也會包含詳細的步驟 tooperform StorSimple 虛擬陣列上的項目層級復原設定為檔案伺服器。

## <a name="clone-shares-from-a-backup-set"></a>從備份組複製共用

**您嘗試 tooclone 共用之前，請確定您有足夠的空間 hello 裝置 toocomplete 這項作業。** 從備份中 hello tooclone [Azure 入口網站](https://portal.azure.com/)，執行下列步驟的 hello。

#### <a name="tooclone-a-share"></a>tooclone 共用

1. 瀏覽過**裝置**刀鋒視窗。 選取並按一下您的裝置，然後按一下共用。 選取您想 tooclone，以滑鼠右鍵按一下 hello 共用 tooinvoke hello 內容功能表的 hello 共用。 選取 [複製]。
   
   ![複製備份](./media/storsimple-virtual-array-clone/cloneshare1.png)
2. 在 hello**複製**刀鋒視窗中，按一下**備份 > 選取**和執行然後 hello 遵循： 
   
   a.    篩選這個 hello 時間範圍為基礎的裝置上的備份。 您可以選擇 [過去 7 天]、[過去 30 天] 和 [過去一年]。
   
   b.    Hello 在清單中顯示篩選過的備份，選取 從備份 tooclone。
   
   c.    按一下 [確定] 。
   
   ![複製備份](./media/storsimple-virtual-array-clone/cloneshare3.png)
3. 在 hello**複製**刀鋒視窗中，按一下 **目標設定**和執行然後 hello 遵循：
   
   a.    提供共用名稱。 hello 共用名稱必須包含 3-127 個字元。
   
   b.    選擇性地提供 hello 複製共用的描述。
   
   c.    您無法變更您要還原到 hello 共用 hello 類型。 階層式共用會複製為階層式，固定在本機的共用則會還原為固定在本機。
   
   d.    hello 容量設定為等於 toohello hello 您正在從複製的共用大小。
   
   e.    指派此共用的 hello 系統管理員。 Hello 複製完成之後，您將無法透過 [檔案總管] 可以 toomodify hello 共用屬性。
   
   f.    按一下 [確定] 。
   
   ![複製備份](./media/storsimple-virtual-array-clone/cloneshare6.png)

4. 按一下**複製**toostart 的複製工作。 Hello 工作完成後，hello 複製作業開始，您會收到通知。 複本上，移 toohello toomonitor hello 進度**作業**刀鋒視窗，然後按一下 hello 作業 tooview 工作詳細資料。
5. 已成功建立 hello 複製之後，瀏覽後 toohello**共用**刀鋒視窗，在您的裝置上。
6. 您現在可以檢視共用 hello 清單中的 hello 新複製的共用您的裝置上。 階層式共用會複製為階層式，固定在本機的共用則會複製為固定在本機的共用。
   
   ![複製備份](./media/storsimple-virtual-array-clone/cloneshare10.png)

## <a name="clone-volumes-from-a-backup-set"></a>從備份組複製磁碟區

tooclone，從備份中 hello Azure 入口網站時，您有 tooperform 步驟類似 toohello 的複製共用。 hello 複製作業複製 hello 備份 tooa 新的磁碟區上 hello 相同的虛擬裝置。您無法再製 tooa 不同的裝置。

#### <a name="tooclone-a-volume"></a>tooclone 磁碟區

1. 瀏覽過**裝置**刀鋒視窗。 選取並按一下您的裝置，然後按一下磁碟區。 選取您想 tooclone，以滑鼠右鍵按一下 hello 磁碟區 tooinvoke hello 內容功能表的 hello 磁碟區。 選取 [複製]。
   
   ![複製磁碟區](./media/storsimple-virtual-array-clone/clonevolume1.png)
2. 在 hello**複製**刀鋒視窗中，按一下**備份**和執行然後 hello 遵循： 
   
   a.    篩選這個 hello 時間範圍為基礎的裝置上的備份。 您可以選擇 [過去 7 天]、[過去 30 天] 和 [過去一年]。 
   
   b.    Hello 在清單中顯示篩選過的備份，選取 從備份 tooclone。
   
   c.    按一下 [確定] 。
   
   ![複製備份](./media/storsimple-virtual-array-clone/clonevolume3.png)
3. 在 hello**複製**刀鋒視窗中，按一下**目標磁碟區設定**和執行然後 hello 遵循::
   
   a. 自動填入 hello 裝置名稱。
   
   b. 提供磁碟區名稱 hello**複製磁碟區**。 hello 磁碟區名稱必須包含 3 too127 個字元。
   
   c. hello 磁碟區類型會自動設定 toohello 原始磁碟區。 階層式磁碟區會複製為階層式，固定在本機的磁碟區則會複製為固定在本機。
   
   d. Hello**連線主機**，按一下 **選取**。
   
   ![複製備份](./media/storsimple-virtual-array-clone/clonevolume4.png)
4. 在 hello**連線主機**刀鋒視窗中，選取 從現有的 ACR，或加入新的 ACR。 tooadd 新的 ACR，您將需要 tooprovide ACR 名稱和 hello 主機 IQN。 按一下 [選取] 。
   
   ![複製備份](./media/storsimple-virtual-array-clone/clonevolume5.png)
5. 按一下**複製**toolaunch 的複製工作。
   
   ![複製備份](./media/storsimple-virtual-array-clone/clonevolume6.png)  
6. Hello 再製工作建立之後，複製會啟動。 一旦建立 hello 複製時，它會顯示 hello 在裝置上的磁碟區 刀鋒視窗。 請注意，階層式磁碟區會複製為階層式，固定在本機的磁碟區則會複製為固定在本機的磁碟區。
   
   ![複製備份](./media/storsimple-virtual-array-clone/clonevolume8.png)
7. Hello 磁碟區出現 online 上的磁碟區的 hello 清單時，hello 磁碟區是可供使用。 Hello iSCSI 啟動器在主機上，重新整理 hello iSCSI 啟動器屬性 視窗中的目標清單。 包含 hello 複製的磁碟區名稱的新目標應該為 'inactive' hello 狀態 欄位會出現。
8. 選取 hello 目標，然後按一下 **連接**。 Hello 啟動器連接的 toohello 目標之後，hello 狀態應該變更太**Connected**。
9. 在 hello**磁碟管理**視窗中，hello 掛接的磁碟區會顯示 hello 下列圖例所示。 以滑鼠右鍵按一下探索到的 hello 磁碟區 （按一下 hello 磁碟名稱），然後按一下**線上**。

> [!IMPORTANT]
> 當嘗試 tooclone，磁碟區或共用從備份集，如果 hello 複製工作失敗、 目標磁碟區或共用仍可能在 hello 入口網站中建立。 請務必您刪除這個目標磁碟區或共用的 hello 入口 toominimize 從這個項目造成任何未來問題。
> 
> 

## <a name="item-level-recovery-ilr"></a>項目層級復原 (ILR)

此版本導入上設定為檔案伺服器的 StorSimple Virtual Array hello 項目層級復原 (ILR)。 hello 功能可讓您 toodo 的精細復原檔案和資料夾從雲端備份的所有 hello 共用 hello StorSimple 裝置上。 您可以使用自助式模型，從最新的備份中擷取已刪除的檔案。

每個共用*.backups*包含 hello 最新備份的資料夾。 您可以瀏覽 toohello 想要的備份、 複製相關的檔案和資料夾從 hello 備份和還原它們。 這項功能就不會呼叫 tooadministrators 從備份還原檔案。

1. 當執行 hello ILR，您可以檢視透過 [檔案總管] 中的 hello 備份。 按一下您想要在 hello 備份 toolook hello 特定共用。 您會看到*.backups* hello 共用儲存所有 hello 備份之下建立資料夾。 展開 hello *.backups*資料夾 tooview hello 備份。 hello 資料夾會顯示 hello hello 整個備份的階層式檢視。 此檢視會建立依需求，並通常會採用只有少數幾秒 toocreate。
   
   hello 最後五個備份以這種方式顯示，而且可以是使用的 tooperform 項目層級復原。 hello 五個最新備份同時包含 hello 預設的排程和 hello 手動備份。
   
   * **排程備份**，命名為 &lt;裝置名稱&gt;DailySchedule-YYYYMMDD-HHMMSS-UTC。
   * **手動備份** ，命名為 Ad-hoc-YYYYMMDD-HHMMSS-UTC。
     
     ![](./media/storsimple-virtual-array-clone/image14.png)

2. 識別 hello 備份，其中包含 hello hello 刪除檔案的最新的版本。 雖然 hello 資料夾名稱包含 UTC 時間戳記在每個 hello 上述情況下，建立資料夾的哪些 hello hello 時間會是 hello 實際裝置 hello 備份開始的時間。 使用 hello 資料夾時間戳記 toolocate，並找出 hello 備份。

3. 找出 hello 資料夾或您想在 hello 備份您所識別的 toorestore hello 上一個步驟中的 hello 檔案。 請注意，您只能檢視 hello 檔案或資料夾的擁有權限。 如果您無法存取某些檔案或資料夾，請連絡共用系統管理員。 hello 系統管理員可以使用檔案總管 tooedit hello 共用權限，並可讓您存取 toohello 特定檔案或資料夾。 它是建議的最佳作法 hello 共用系統管理員的使用者群組，而不是單一使用者。

4. 複製 hello 檔案或 hello 資料夾 toohello 適當的共用您的 StorSimple 檔案伺服器上。

## <a name="next-steps"></a>後續步驟

深入了解如何太[管理使用本機 web UI hello 您 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md)。

