---
title: "在 StorSimple Virtual Array 上安裝 Update 0.5 | Microsoft Docs"
description: "描述如何透過 StorSimple Virtual Array Web UI，使用 Azure 入口網站和 Hotfix 方法套用更新"
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
ms.date: 05/10/2017
ms.author: alkohli
ms.openlocfilehash: c47da5b90c16e2d5b5709e2a6affc026238b9468
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="install-update-05-on-your-storsimple-virtual-array"></a>在 StorSimple Virtual Array 上安裝 Update 0.5

## <a name="overview"></a>概觀

此文章說明透過本機 Web UI 和透過 Azure 入口網站在 StorSimple Virtual Array 上安裝 Update 0.5 時所需的步驟。 您需要套用軟體更新或 Hotfix，以便讓您的 StorSimple Virtual Array 保持在最新狀態。

套用更新之前，建議您先讓主機上的磁碟區或共用離線，再讓裝置離線。 這樣可以讓資料損毀的可能性降至最低。 磁碟區或共用離線之後，您也應該手動備份裝置。

> [!IMPORTANT]
> - Update 0.5 對應至您裝置上的 10.0.10290.0 軟體版本。 如需此更新中新功能的資訊，請移至 [Update 0.5 的版本資訊 (英文)](storsimple-virtual-array-update-05-release-notes.md)。
>
> - 如果您執行的是 Update 0.2 或更新版本，建議您透過 Azure 入口網站安裝更新。 如果您正在執行 Update 0.1 或 GA 軟體版本，您就必須透過本機 Web UI 使用 Hotfix 方法來安裝 Update 0.5。
>
> - 請記住，安裝更新或 Hotfix 會重新啟動您的裝置。 假設 StorSimple Virtual Array 是單一節點裝置，就會中斷任何進行中的 I/O，裝置也會停機。

## <a name="use-the-azure-portal"></a>使用 Azure 入口網站

如果執行 Update 0.2 或更新版本，建議您透過 Azure 入口網站安裝更新。 入口網站的程序需要使用者掃描、下載然後安裝更新。 此程序需要大約 7 分鐘才能完成。 請執行下列步驟以安裝更新或 Hotfix。

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

安裝完成後，請移至 StorSimple 裝置管理員服務。 選取 [裝置]，然後選取並按一下您剛剛更新的裝置。 移至 [設定] > [管理] > [裝置更新]。 顯示的軟體版本應該是 10.0.10290.0。

## <a name="use-the-local-web-ui"></a>使用本機 Web UI

使用本機 Web UI 時有兩個步驟︰

* 下載更新或 Hotfix
* 安裝更新或 Hotfix

### <a name="download-the-update-or-the-hotfix"></a>下載更新或 Hotfix

請執行下列步驟，從 Microsoft Update Catalog 下載軟體更新。

#### <a name="to-download-the-update-or-the-hotfix"></a>下載更新或 Hotfix

1. 啟動 Internet Explorer 並瀏覽至 [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com)。

2. 如果這是您第一次在此電腦上使用 Microsoft Update Catalog，請在系統提示您安裝 Microsoft Update Catalog 附加元件時，按一下 [安裝]  。

3. 在 Microsoft Update Catalog 的搜尋方塊中，輸入您要下載的 Hotfix 知識庫 (KB) 編號。 輸入 **4021576** (適用於 Update 0.5)，然後按一下 [搜尋]。
   
    此時會顯示 Hotfix 清單，例如 StorSimple Virtual Array Update 0.5。
   
    ![搜尋目錄](./media/storsimple-virtual-array-install-update-05/download1.png)

4. 按一下 [下載] 。 

5. 您應該會看到下載兩個檔案，分別是 .msu 與 .cab 檔案。 將這兩個檔案一一下載至資料夾。 資料夾也可以複製到裝置可連線的網路共用位置。

6. 開啟檔案所在的資料夾。
    ![封裝中的檔案](./media/storsimple-virtual-array-install-update-05/update05folder.png)

    您會看見：
    -  Microsoft Update 獨立封裝檔案`WindowsTH-KB3011067-x64`。 此檔案用來更新裝置軟體。
    - Geneva 監視代理程式封裝檔案`GenevaMonitoringAgentPackageInstaller`。 此檔案用於更新「監視與診斷」服務 (MDS) 代理程式。 按兩下 cab 檔案。 隨即顯示 .msi。 選取檔案，按一下滑鼠右鍵，然後按一下 [擷取] 以擷取檔案。 您將使用.msi 檔案更新代理程式。

        ![擷取 MDS 代理程式更新檔案](./media/storsimple-virtual-array-install-update-05/extract-geneva-monitoring-agent-installer.png)
        
    

### <a name="install-the-update-or-the-hotfix"></a>安裝更新或 Hotfix

安裝更新或 Hotfix 之前，請確定更新或 Hotfix 已下載至您主機的本機上，或是可透過網路共用存取。

請使用此方法在執行 GA 或 Update 0.1 軟體版本的裝置上安裝更新。 此程序需時不到 2 分鐘。 請執行下列步驟以安裝更新或 Hotfix。

#### <a name="to-install-the-update-or-the-hotfix"></a>安裝更新或 Hotfix

1. 在本機 Web UI 中，移至 [維護]  >  [軟體更新]。
   
    ![更新裝置](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. 在 [更新檔案路徑] 中，輸入更新或 Hotfix 的檔案名稱。 如果更新或 Hotfix 的安裝檔案是放在網路共用上，您也可以瀏覽至該檔案。 按一下 [Apply (套用)] 。
   
    ![更新裝置](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. 此時會顯示警告。 如果這是單一節點裝置，在套用更新後，裝置就會重新啟動而會有停機時間。 按一下核取圖示。
   
   ![更新裝置](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. 更新會開始進行。 成功更新裝置之後，裝置就會重新啟動。 在這段持續時間會無法存取本機 UI。
   
    ![更新裝置](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. 重新啟動完成後，您就會進入 [登入] 頁面。 若要確認裝置軟體是否已更新，請在本機 Web UI 中，移至 [維護]  >  [軟體更新]。 顯示的軟體版本應該是 10.0.0.0.0.10290.0 (適用於 Update 0.5)。
   
   > [!NOTE]
   > 我們在本機 Web UI 和 Azure 入口網站中回報軟體版本的方式略有不同。 例如，本機 Web UI 會回報 10.0.0.0.0.10290，而相同版本在 Azure 入口網站則會回報為 10.0.10290.0。
   
    ![更新裝置](./media/storsimple-virtual-array-install-update-05/update6m.png)

6. 下一個步驟是更新 MDS 代理程式。 在 [軟體更新] 頁面上，移至 [更新檔案路徑]，然後瀏覽至 `GenevaMonitoringAgentPackageInstaller.msi` 檔案。 重複步驟 2 至 4。 虛擬陣列重新啟動之後，登入本機 Web UI。

更新現已完成。

## <a name="next-steps"></a>後續步驟

深入了解 [administering your StorSimple Virtual Array (管理 StorSimple Virtual Array)](storsimple-ova-web-ui-admin.md)。

