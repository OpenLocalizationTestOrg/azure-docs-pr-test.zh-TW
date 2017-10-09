---
title: "更新 StorSimple Virtual Array 0.6 aaaInstall |Microsoft 文件"
description: "描述如何 toouse hello StorSimple Virtual Array web UI tooapply 更新使用 hello Azure 入口網站與 hotfix 方法"
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
ms.workload: TBD
ms.date: 05/18/2017
ms.author: alkohli
ms.openlocfilehash: 2ccd1b5fc1957c35ebec35aa947d331b3ff05464
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-06-on-your-storsimple-virtual-array"></a>在 StorSimple Virtual Array 上安裝 Update 0.6

## <a name="overview"></a>概觀

本文說明 hello 步驟需要的 tooinstall 更新 0.6 StorSimple 虛擬陣列透過 hello 本機 web UI 中和透過 hello Azure 入口網站上。 您最新的 StorSimple Virtual Array 套用 hello 軟體更新或 hotfix tookeep。

在套用更新之前，我們建議您採取 hello 磁碟區或離線 hello 上的共用裝載第一次，然後 hello 裝置。 這樣可以讓資料損毀的可能性降至最低。 Hello 磁碟區或共用離線之後，您也應該採取手動 hello 裝置的備份。

> [!IMPORTANT]
> - 更新 0.6 對應太**10.0.10293.0**在裝置上的軟體版本。 如需此更新中新功能的資訊，請移至太[0.6 更新的版本資訊](storsimple-virtual-array-update-06-release-notes.md)。
>
> - 如果您正在更新 0.2 或更新版本中，我們建議您安裝 hello 透過 hello Azure 入口網站的更新。 如果您執行 Update 0.1 或 GA 軟體版本，您必須使用透過 hello 本機 web UI tooinstall 更新 0.6 hello hotfix 方法。
>
> - 請記住，安裝更新或 Hotfix 會重新啟動您的裝置。 指定 hello StorSimple Virtual Array 是單一節點的裝置、 任何進行中的 I/O 中斷和您的裝置會發生停機。

## <a name="use-hello-azure-portal"></a>使用 hello Azure 入口網站

如果 0.2 和更新版本，請執行更新，我們建議您安裝透過 hello Azure 入口網站的更新。 hello 入口網站的程序需要 hello 使用者 tooscan、 下載及安裝 hello 的更新。 此程序接受 toocomplete 大約 7 分鐘。 執行 hello 下列步驟 tooinstall hello 更新或 hotfix。

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

Hello 之後安裝已完成，請移 tooyour StorSimple 裝置管理員服務。 選取**裝置**然後選取並按一下您剛才更新 hello 裝置。 跳過**設定 > 管理 > 裝置更新**。 hello 顯示軟體版本應為**10.0.10293.0**。

## <a name="use-hello-local-web-ui"></a>使用 hello 本機 web UI

使用 hello 本機 web UI 時，有兩個步驟：

* 下載 hello 更新或 hello hotfix
* 安裝 hello 更新或 hello hotfix

### <a name="download-hello-update-or-hello-hotfix"></a>下載 hello 更新或 hello hotfix

執行 hello hello Microsoft Update 類別目錄中的下列步驟 toodownload hello 軟體更新。

#### <a name="toodownload-hello-update-or-hello-hotfix"></a>toodownload hello update 或 hello hotfix

1. 啟動 Internet Explorer 並瀏覽過[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com)。

2. 如果您使用 Microsoft Update 類別目錄 hello hello 第一次在這部電腦上，按一下**安裝**時提示的 tooinstall hello Microsoft Update 類別目錄的附加元件。

3. 在 hello hello Microsoft Update 類別目錄的搜尋方塊中輸入 hello 知識庫 (KB) 號碼要 toodownload 的 hello hotfix。 輸入 **4023268** (適用於 Update 0.6)，然後按一下搜尋。
   
    hello hotfix 清單會出現，例如**StorSimple 虛擬陣列更新 0.6**。
   
    ![搜尋目錄](./media/storsimple-virtual-array-install-update-06/download1.png)

4. 按一下 [下載] 。

5. 您應該會看到五個檔案 toodownload。 下載每個這些檔案 tooa 資料夾。 hello 資料夾也可以複製的 tooa 從 hello 裝置的網路共用。

6. 開啟 hello hello 檔案所在資料夾。
    ![Hello 套件中的檔案](./media/storsimple-virtual-array-install-update-06/update06folder.png)

    您會看見：
    -  Microsoft Update 獨立封裝檔案`WindowsTH-KB3011067-x64`。 這個檔案是使用的 tooupdate hello 裝置軟體。
    - Geneva 監視代理程式封裝檔案`GenevaMonitoringAgentPackageInstaller`。 這個檔案是使用的 tooupdate hello 監視和診斷服務 (MDS) 代理程式。 按兩下 hello 封包檔。 隨即顯示 _.msi_。 選取 hello 檔案按一下滑鼠右鍵，然後**擷取**hello 檔案。 使用 hello _.msi_檔案 tooupdate hello 代理程式。

        ![擷取 MDS 代理程式更新檔案](./media/storsimple-virtual-array-install-update-06/extract-geneva-monitoring-agent-installer.png)

        > [!IMPORTANT]
        > 如果您執行 StorSimple 更新 0.5 (0.0.10293.0) 不需要 tooupdate hello MDS 代理程式。

    - 包含 Windows 重大安全性更新的三個檔案：`windows8.1-kb4012213-x64`、`windows8.1-kb3205400-x64` 和 `windows8.1-kb4019213-x64`。


### <a name="install-hello-update-or-hello-hotfix"></a>安裝 hello 更新或 hello hotfix

先前 toohello 更新或 hotfix 安裝，請確定您擁有 hello 更新，或 hello hotfix 下載您的主機上的本機或透過網路共用。

執行 GA 的裝置上使用這個方法會 tooinstall 更新或更新 0.1 軟體版本。 此程序會取用大約 12 分鐘 toocomplete。 執行 hello 下列步驟 tooinstall hello 更新或 hotfix。

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a>tooinstall hello update 或 hello hotfix

1. 在本機 web UI hello，移過**維護** > **軟體更新**。 記下您所執行的 hello 軟體版本。 如果您正在**10.0.10290.0**，您不需要 tooupdate hello MDS 代理程式在步驟 6。
   
    ![更新裝置](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. 在**更新檔案路徑**、 輸入 hello hello 更新的檔案名稱或 hello hotfix。 如果放在網路共用上，您也可以瀏覽 toohello 更新或 hotfix 安裝檔案。 按一下 [Apply (套用)] 。
   
    ![更新裝置](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. 此時會顯示警告。 指定的 hello 虛擬陣列是單一節點裝置之後套用 hello 更新，hello 裝置重新啟動，且沒有停機時間。 按一下 [hello] 核取圖示。
   
   ![更新裝置](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. hello 更新開始。 已成功更新 hello 裝置之後，它會重新啟動。 hello 本機 UI 不能存取在此期間。
   
    ![更新裝置](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. Hello 重新啟動完成之後，即會進入 toohello**登入**頁面。 更新 hello 裝置軟體，在 hello 本機 web UI，tooverify 移過**維護** > **軟體更新**。 hello 顯示軟體版本應為**10.0.0.0.0.10293**更新 0.6。
   
   > [!NOTE]
   > 我們稍有不同的方式，在 hello 本機 web UI 中會報告 hello 軟體版本及 hello Azure 入口網站。 例如，hello 本機 web UI 報告**10.0.0.0.0.10293** hello Azure 入口網站的報表和**10.0.10293.0** hello 相同版本。
   
    ![更新裝置](./media/storsimple-virtual-array-install-update-06/update6m.png)

6. 如果套用此更新前執行的是 StorSimple Virtual Array Update 0.5 (**10.0.10290.0**)，請跳過此步驟。 開始 tooupdate 前，您可以進行步驟 1 中的 hello 軟體版本的附註。 如果之前執行的是 Update 0.5，MDS 代理程式已經是最新版。

    如果您正在執行軟體版本先前 tooUpdate 0.5，hello 為您的下一個步驟是 tooupdate hello MDS 代理程式。 在 hello**軟體更新**頁面上，移 toohello**更新檔案路徑**並瀏覽 toohello`GenevaMonitoringAgentPackageInstaller.msi`檔案。 重複步驟 2 至 4。 Hello 虛擬陣列重新啟動之後，登入 hello 本機 web UI。

7. 重複步驟 2-4 tooinstall hello Windows 安全性修正使用檔案`windows8.1-kb4012213-x64`，`windows8.1-kb3205400-x64`，和`windows8.1-kb4019213-x64`。 hello 虛擬陣列會在每次安裝之後，您需要 toosign 入 hello 本機 web UI。

## <a name="next-steps"></a>後續步驟

深入了解 [administering your StorSimple Virtual Array (管理 StorSimple Virtual Array)](storsimple-ova-web-ui-admin.md)。

