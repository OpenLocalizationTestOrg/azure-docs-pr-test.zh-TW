---
title: "aaaStorSimple 8000 系列 Update 3 版本資訊 |Microsoft 文件"
description: "適用於 StorSimple 8000 系列 Update 3 描述 hello 新功能、 問題和因應措施。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 2158aa7a-4ac3-42ba-8796-610d1adb984d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5bfcba61f7f210531437f650eafaad4dbd8c7c45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="update-3-release-notes-for-your-storsimple-8000-series-device"></a>StorSimple 8000 系列裝置的 Update 3 版本資訊

## <a name="overview"></a>概觀
hello 下列版本資訊描述 hello 新功能和適用於 StorSimple 8000 系列 Update 3 中識別 hello 重要的議題。 也會包含在此版本中所包含的 hello StorSimple 軟體更新清單。 

Update 3 可以透過更新 2.2 執行版本 (GA) 或 Update 0.1 套用的 tooany StorSimple 裝置。 Update 3 與相關聯的 hello 裝置版本是 6.3.9600.17759。

請檢閱附註，然後再部署 hello 更新您的 StorSimple 解決方案中的 hello 版本中所包含的 hello 資訊。

> [!IMPORTANT]
> * Update 3 包含裝置軟體、LSI 驅動程式和韌體以及 Storport 和 Spaceport 的更新。 它會採用大約 1.5-2 小時 tooinstall 這項更新。 
> * 新的版本，您可能不會看到更新立即，因為我們會執行 hello 更新分階段導入。 請等候數天然後再次掃描更新，因為很快就會提供更新。
> 
> 

## <a name="whats-new-in-update-3"></a>Update 3 的新功能
hello 下列索引鍵的改進和 bug 修正可能已在 Update 3。

* **自動化空間回收變更**– 在 hello 系統產生更快的執行中的 hello 待命控制器上執行的啟動 Update 3，hello 空間回收演算法。 如需有關必要之空間回收 toowork hello 通訊埠的詳細資訊，請參閱 toohello[網路需求的 StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device)。
* **效能增強功能**– Update 3 已改善讀寫效能 toohello 雲端。
* **移轉相關的增強功能**– 在此版本中，數個錯誤修正和增強功能從 5000/7000 系列裝置 too8000 系列的裝置時進行 hello 移轉功能。 如需有關如何 toouse hello 移轉功能的詳細資訊，請移太[從 5000/7000 系列裝置 too8000 系列裝置的移轉](https://gallery.technet.microsoft.com/Azure-StorSimple-50007000-c1a0460b)。 
* **監視相關的修正**-在此版本中，相關 toomonitoring 圖表 」、 「 服務儀表板和 「 裝置儀表板已修正的 bug。

## <a name="issues-fixed-in-update-3"></a>Update 3 中修正的問題
hello 下表提供摘要的 Update 3 中已修正的問題。    

| 否 | 功能 | 問題 | 適用於 toophysical 裝置 | 適用於 toovirtual 裝置 |
| --- | --- | --- | --- | --- |
| 1 |主機端資料移轉 |Hello 中先前的版本，hello StorSimple 雲端應用裝置已離線主機端的資料移轉期間。 此版本已經修正這個問題。 |否 |是 |
| 2 |固定在本機的磁碟區 |在 hello 先前版本中，沒有相關的 tooI/O 失敗問題，磁碟區轉換失敗，本機固定磁碟區的資料路徑失敗。 此版本已找出這些問題的根本原因並加以修正。 |是 |否 |
| 3 |監視 |有多個問題相關的 tooreporting 單位而且監視器以及裝置儀表板圖表，其中不正確的資訊已顯示在本機固定磁碟區。 此版本已經修正這些問題。 |是 |否 |
| 4 |大量寫入 I/O |當使用 StorSimple 涉及大量寫入的工作負載，hello 使用者會發生不頻繁的 bug 其中 hello 工作集分層到 hello 的雲端。 此版本已經修正這個錯誤。 |是 |是 |
| 5 |備份 |在某些罕見的情況，在 hello 舊版的軟體，當使用者進行的遠端複本的備份，就會發生定域機組錯誤和 hello 作業會將錯誤傳出。在此版本中，修正 hello 問題和 hello 作業順利完成。 |是 |是 |
| 6 |備份原則 |在某些罕見的情況，在 hello 舊版的軟體，時發生 bug 相關 toohello 刪除備份原則。 此版本已經修正這個問題。 |是 |是 |

## <a name="known-issues-in-update-3"></a>Update 3 中的已知問題
hello 下表提供此版本已知問題的摘要。

| 否。 | 功能 | 問題 | 註解 / 因應措施 | 適用於 toophysical 裝置 | 適用於 toovirtual 裝置 |
| --- | --- | --- | --- | --- | --- |
| 1 |磁碟仲裁 |在罕見情況下，如果 hello 大多數的 8600 裝置 hello EBOD 機箱中的磁碟中斷連線，以致於沒有磁碟仲裁，然後 hello 存放集區會離線。 即使 hello 磁碟重新連接會保持離線。 |您將需要 tooreboot hello 裝置。 如果 hello 問題持續發生，請連絡 Microsoft 支援以取得後續步驟。 |是 |否 |
| 2 |不正確的控制器識別碼 |進行控制器更換時，控制器 0 可能顯示為控制器 1。 控制器更換期間，從 hello 對等節點，載入 hello 映像時 hello 控制器識別碼最初可能顯示為 hello 同儕節點控制器的識別碼。 在罕見情況下，可能會在系統重新開機後出現這種行為。 |因此，使用者不需要採取任何動作。 Hello 控制器更換完成之後，這種情況下將自行解決。 |是 |否 |
| 3 |儲存體帳戶 |使用 hello 儲存體服務 toodelete hello 儲存體帳戶是不支援的案例。 這會導致無法擷取使用者資料所在的 tooa 情況。 | |是 |是 |
| 4 |裝置容錯移轉 |磁碟區容器從相同來源裝置 toodifferent 目標裝置不支援的 hello 的多個容錯移轉。 從單一失效裝置 toomultiple 裝置容錯移轉會使 hello 磁碟區容器上第一次容錯移轉裝置 hello 喪失資料擁有權。 這類容錯移轉之後，這些磁碟區容器將會出現，或當您在 hello Azure 傳統入口網站中檢視時有不同的行為。 | |是 |否 |
| 5 |安裝 |在 StorSimple Adapter for SharePoint 安裝，您必須 tooprovide 裝置 IP，為了讓 hello 安裝 toofinish 成功。 | |是 |否 |
| 6 |Web Proxy |如果您的 web proxy 組態已 HTTPS 做為 hello 指定通訊協定，則您裝置到服務的通訊會受到影響並且 hello 裝置會離線。 在 hello 過程中，使用您的裝置上的大量資源，也會產生支援封裝。 |請確定 hello web proxy URL 有 HTTP，如 hello 指定的通訊協定。 如需詳細資訊，請移至太[設定 web proxy 為您的裝置](storsimple-configure-web-proxy.md)。 |是 |否 |
| 7 |Web Proxy |如果您設定並啟用 web proxy 註冊的裝置上，您會在您的裝置上需要 toorestart hello 作用中控制器。 | |是 |否 |
| 8 |雲端高延遲與高 I/O 工作負載 |當您的 StorSimple 裝置發生極高雲端延遲 （秒數的順序） 和高 I/O 工作負載的組合時，hello 裝置磁碟區會進入降級狀態，而 hello I/o 可能會因 「 裝置未就緒 」 錯誤。 |您將會需要 toomanually 重新開機 hello 裝置控制器或執行裝置容錯移轉 toorecover 從這種情況。 |是 |否 |
| 9 |Azure PowerShell |當您使用 hello StorSimple cmdlet **Get AzureStorSimpleStorageAccountCredential &#124;Select-object-先 1-等候**tooselect hello 第一個物件，好讓您可以建立新**磁碟區容器**物件 hello cmdlet 會傳回所有的 hello 物件。 |將 hello cmdlet 包裝在括號，如下所示： **(Get-Azure-StorSimpleStorageAccountCredential) &#124;Select-object-先 1-等候** |是 |是 |
| 10 |移轉 |移轉傳遞多個磁碟區容器，hello 知道最新備份時，只為第一個磁碟區容器 hello 精確。 此外，hello hello 第一個磁碟區容器中的前 4 個備份移轉之後，會進行平行的移轉。 |建議您一次移轉一個磁碟區容器。 |是 |否 |
| 11 |移轉 |Hello 還原之後，磁碟區不會新增 toohello 備份原則或 hello 虛擬磁碟群組。 |您將需要 tooadd 順序 toocreate 備份這些磁碟區 tooa 備份原則。 |是 |是 |
| 12 |移轉 |Hello 移轉完成之後，hello 5000/7000 系列裝置不得存取 hello 移轉資料容器。 |我們建議您刪除 hello hello 移轉便會完成認可之後，移轉資料容器。 |是 |否 |
| 13 |複製和 DR |執行 Update 1 的 StorSimple 裝置無法複製或執行災害復原 tooa 裝置執行更新前 1 軟體。 |您將需要 tooupdate hello 目標裝置 tooUpdate 1 tooallow 這些作業 |是 |是 |
| 14 |移轉 |當磁碟區群組中沒有相關聯的磁碟區時，5000-7000 系列裝置上用於移轉的設定備份可能會失敗。 |刪除所有 hello 空的磁碟區群組與沒有相關聯的磁碟區，然後再重試 hello 設定備份。 |是 |否 |
| 15 |Azure PowerShell Cmdlet 和固定在本機的磁碟區 |您無法透過 Azure PowerShell Cmdlet 建立固定在本機的磁碟區。 (您透過 Azure PowerShell 建立的任何磁碟區都會分層。) |一律使用 hello StorSimple Manager 服務 tooconfigure 固定在本機磁碟區。 |是 |否 |
| 16 |固定在本機的磁碟區的可用空間 |如果您刪除本機固定磁碟區，可能不會立即更新 hello 空間供新磁碟區。 hello StorSimple Manager 服務更新 hello 約每小時的可用本機空間。 |等候一小時，然後再試 toocreate hello 新磁碟區。 |是 |否 |
| 17 |固定在本機的磁碟區 |還原作業會公開 hello hello 備份類別目錄，但只在 hello hello 還原作業期間暫時快照集備份。 此外，它會公開具有前置詞的虛擬磁碟群組**tmpCollection**上 hello**備份原則**頁面上，但只會針對 hello hello 期間還原作業。 |如果還原作業僅有固定在本機的磁碟區或是混合了固定在本機的磁碟區與分層磁碟區，就可能就會發生此問題。 如果 hello 還原工作包含只有分層磁碟區，將不會發生這個問題。 不需使用者介入。 |是 |否 |
| 18 |固定在本機的磁碟區 |如果您取消還原作業，而且控制器容錯移轉發生之後，將會顯示 hello 還原作業**失敗**而不是**Canceled**。 如果還原作業失敗，且控制器容錯移轉發生之後，將會顯示 hello 還原作業**Canceled**而不是**失敗**。 |如果還原作業僅有固定在本機的磁碟區或是混合了固定在本機的磁碟區與分層磁碟區，就可能就會發生此問題。 如果 hello 還原工作包含只有分層磁碟區，將不會發生這個問題。 不需使用者介入。 |是 |否 |
| 19 |固定在本機的磁碟區 |如果您取消還原作業，或如果還原失敗，則控制器容錯移轉會發生其他還原工作會出現在 hello**作業**頁面。 |如果還原作業僅有固定在本機的磁碟區或是混合了固定在本機的磁碟區與分層磁碟區，就可能就會發生此問題。 如果 hello 還原工作包含只有分層磁碟區，將不會發生這個問題。 不需使用者介入。 |是 |否 |
| 20 |固定在本機的磁碟區 |如果 tooconvert 分層磁碟區 （建立和複製與更新 1.2 或更早版本） 再試一次 tooa 本機固定磁碟區，而且您的裝置空間不足或在雲端中斷，則 hello clone(s) 可能會損毀。 |此問題只發生於使用 Update 2.1 之前的軟體所建立及複製的磁碟機。 這應該是不常見的案例。 | | |
| 21 |磁碟區轉換 |不會更新 hello Acr 附加的 tooa 磁碟區磁碟區轉換正在進行時 (釘選的分層式的 toolocally，反之亦然)。 更新 hello Acr，可能會導致資料損毀。 |如有需要更新 hello Acr 先前 toohello 磁碟區轉換並且不要讓任何進一步的 ACR 更新 hello 轉換正在進行時。 | | |
| 22 |更新 |當套用 Update 3，hello**維護**hello Azure 傳統入口網站會在頁面上顯示 hello 以下訊息相關的 tooUpdate 2-「 StorSimple 8000 系列 Update 2 包含 Microsoft tooproactively 收集 hello 能力記錄資訊從您的裝置時偵測到潛在的問題 」。 這會產生誤導，因為它會指出該 hello 裝置正在更新的 tooUpdate 2。 Hello 裝置更新 succeesfully tooUpdate 3 後，此訊息會消失。 |在未來版本中將會修正這個行為。 |是 |否 |

## <a name="controller-and-firmware-updates-in-update-3"></a>Update 3 中的控制器和韌體更新
此版本包含 LSI 驅動程式和韌體更新。 如需有關如何 tooinstall hello LSI 驅動程式與韌體更新，請參閱[安裝 Update 3](storsimple-install-update-3.md) StorSimple 裝置上。

## <a name="virtual-device-updates-in-update-3"></a>Update 3 中的虛擬裝置更新
此更新不能套用的 toohello StorSimple 雲端應用裝置 （也稱為 hello 虛擬裝置）。 將新的虛擬裝置必須 toobe 建立。 

## <a name="next-step"></a>後續步驟
了解如何太[安裝 Update 3](storsimple-install-update-3.md) StorSimple 裝置上。

