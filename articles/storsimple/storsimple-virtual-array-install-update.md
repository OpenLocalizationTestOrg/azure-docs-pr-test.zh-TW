---
title: "在 Microsoft Azure StorSimple Virtual Array aaaInstall 更新 |Microsoft 文件"
description: "描述如何 toouse hello StorSimple Virtual Array web UI tooapply 更新使用 hello 入口網站與 hotfix 方法"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 9997a97b-9382-43ed-b56e-61369335c987
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7424abc7e46d4f08b4eae1194642b263f32c4318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array---azure-portal"></a>在 StorSimple Virtual Array 上安裝更新 - Azure 入口網站

## <a name="overview"></a>概觀

本文說明 hello 步驟需要的 tooinstall 更新 StorSimple 虛擬陣列透過 hello 本機 web UI 中和透過 hello Azure 入口網站上。 您需要 tooapply 軟體更新或 hotfix tookeep StorSimple 虛擬陣列最新狀態。 

請記住，安裝更新或 Hotfix 會重新啟動您的裝置。 指定 hello StorSimple Virtual Array 是單一節點的裝置、 任何進行中的 I/O 中斷和您的裝置會發生停機。 

在套用更新之前，我們建議您採取 hello 磁碟區或離線 hello 上的共用裝載第一次，然後 hello 裝置。 這樣可以讓資料損毀的可能性降至最低。

> [!IMPORTANT]
> 如果您執行 Update 0.1 或 GA 軟體版本，您必須使用透過 hello 本機 web UI tooinstall update 0.3 hello hotfix 方法。 如果您正在更新 0.2，我們建議您透過 hello Azure 傳統入口網站的 hello 更新安裝。
 

## <a name="use-hello-local-web-ui"></a>使用 hello 本機 web UI

使用 hello 本機 web UI 時，有兩個步驟：

* 下載 hello 更新或 hello hotfix
* 安裝 hello 更新或 hello hotfix

### <a name="download-hello-update-or-hello-hotfix"></a>下載 hello 更新或 hello hotfix

執行 hello hello Microsoft Update 類別目錄中的下列步驟 toodownload hello 軟體更新。

#### <a name="toodownload-hello-update-or-hello-hotfix"></a>toodownload hello update 或 hello hotfix

1. 啟動 Internet Explorer 並瀏覽過[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com)。

2. 如果這是您第一次使用 hello Microsoft Update 類別目錄，在此電腦上，按一下**安裝**時提示的 tooinstall hello Microsoft Update 類別目錄的附加元件。

3. 在 hello hello Microsoft Update 類別目錄的搜尋方塊中輸入 hello 知識庫 (KB) 號碼要 toodownload 的 hello hotfix。 輸入 **3182061** (適用於 Update 0.3)，然後按一下搜尋。
   
    hello hotfix 清單會出現，例如**StorSimple 虛擬陣列 Update 0.3**。
   
    ![搜尋目錄](./media/storsimple-virtual-array-install-update/download1.png)

4. 按一下 [新增] 。 hello 更新已新增 toohello 籃。

5. 按一下 [ **檢視購物籃**]。

6. 按一下 [下載] 。 指定或**瀏覽**所在 hello 下載 tooappear tooa 本機位置。 hello 下載更新 toohello 指定的位置，並放在名稱為 「 hello 更新相同的 hello 與子資料夾中。 hello 資料夾也可以複製的 tooa 從 hello 裝置的網路共用。

7. 開啟 hello 複製資料夾，您應該會看到 Microsoft Update 獨立封裝檔案`WindowsTH-KB3011067-x64`。 這個檔案是使用的 tooinstall hello 更新或 hotfix。

### <a name="install-hello-update-or-hello-hotfix"></a>安裝 hello 更新或 hello hotfix

先前 toohello 更新或 hotfix 安裝，請確定您擁有 hello 更新，或 hello hotfix 下載您的主機上的本機或透過網路共用。 

執行 GA 的裝置上使用這個方法會 tooinstall 更新或更新 0.1 軟體版本。 此程序接受不超過 2 分鐘 toocomplete。 執行 hello 下列步驟 tooinstall hello 更新或 hotfix。

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a>tooinstall hello update 或 hello hotfix

1. 在本機 web UI hello，移過**維護** > **軟體更新**。
   
    ![更新裝置](./media/storsimple-virtual-array-install-update/update1m.png)

2. 在**更新檔案路徑**、 輸入 hello hello 更新的檔案名稱或 hello hotfix。 如果放在網路共用上，您也可以瀏覽 toohello 更新或 hotfix 安裝檔案。 按一下 [Apply (套用)] 。
   
    ![更新裝置](./media/storsimple-virtual-array-install-update/update2m.png)

3. 此時會顯示警告。 指定這是單一節點裝置之後套用 hello 更新，hello 裝置重新啟動，且沒有停機時間。 按一下 [hello] 核取圖示。
   
   ![更新裝置](./media/storsimple-virtual-array-install-update/update3m.png)

4. hello 更新開始。 已成功更新 hello 裝置之後，它會重新啟動。 hello 本機 UI 不能存取在此期間。
   
    ![更新裝置](./media/storsimple-virtual-array-install-update/update5m.png)

5. Hello 重新啟動完成之後，即會進入 toohello**登入**頁面。 更新 hello 裝置軟體，在 hello 本機 web UI，tooverify 移過**維護** > **軟體更新**。 hello 顯示軟體版本應為**10.0.0.0.0.10288.0** update 0.3。
   
   > [!NOTE]
   > 我們稍有不同的方式，在 hello 本機 web UI 中會報告 hello 軟體版本及 hello Azure 入口網站。 例如，hello 本機 web UI 報告**10.0.0.0.0.10288** hello Azure 入口網站的報表和**10.0.10288.0** hello 相同版本。
   
    ![更新裝置](./media/storsimple-virtual-array-install-update/update6m.png)

## <a name="use-hello-azure-portal"></a>使用 hello Azure 入口網站

如果執行 Update 0.2，我們建議您安裝透過 hello Azure 入口網站的更新。 hello 入口網站的程序需要 hello 使用者 tooscan、 下載及安裝 hello 的更新。 此程序接受 toocomplete 大約 7 分鐘。 執行 hello 下列步驟 tooinstall hello 更新或 hotfix。

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal.md)]

Hello 之後安裝已完成 （示依工作狀態在 100%），請移 tooyour StorSimple 裝置管理員服務。 選取**裝置**然後選取並按一下您想要從裝置連接的 toothis 服務的 hello 清單 tooupdate hello 裝置。 在 hello**設定**刀鋒視窗中，跳過**管理**區段，然後選取**裝置更新**。 hello 顯示軟體版本應為**10.0.10288.0**。


## <a name="next-steps"></a>後續步驟

深入了解 [administering your StorSimple Virtual Array (管理 StorSimple Virtual Array)](storsimple-ova-web-ui-admin.md)。

