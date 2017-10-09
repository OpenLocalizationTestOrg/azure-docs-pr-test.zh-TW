---
title: "aaaStorSimple 8000 系列 Update 2 版本資訊 |Microsoft 文件"
description: "StorSimple 8000 系列 Update 2，描述 hello 新功能、 問題和因應措施。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: e2c8bffd-7fc5-4b77-b632-a4f59edacc3a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 36c75aad900c7b1286a924732967b8ee519a3d4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-2-release-notes"></a>StorSimple 8000 系列 Update 2 版本資訊
## <a name="overview"></a>概觀
hello 下列版本資訊說明 hello 新功能和識別 hello 重大議題 StorSimple 8000 系列 Update 2。 它們也包含一份 hello StorSimple 軟體、 驅動程式，以及在此版本中所包含的磁碟韌體更新。 

Update 2 可以透過更新 1.2 執行版本 (GA) 或 Update 0.1 套用的 tooany StorSimple 裝置。 hello 與 Update 2 相關聯的裝置版本是 6.3.9600.17673。

請檢閱附註，然後再部署 hello 更新您的 StorSimple 解決方案中的 hello 版本中所包含的 hello 資訊。

> [!IMPORTANT]
> * 它會採用大約 4-7 小時 tooinstall 這項更新 （包括 hello Windows 更新）。 
> * Update 2 具有軟體、LSI 驅動程式和 SSD 韌體更新。
> * 新的版本，您可能不會看到更新立即，因為我們會執行 hello 更新分階段導入。 請等候數天然後再次掃描更新，因為很快就會提供更新。
> 
> 

## <a name="whats-new-in-update-2"></a>Update 2 的新功能
Update 2 導入了下列新功能的 hello。

* **固定在本機磁碟區**– 在 hello StorSimple 8000 系列的舊版本中，資料區塊是根據使用方式的階層式的 toohello 雲端。 沒有任何方式 tooguarantee 區塊會儲存在本機的。 在 Update 2 中，當您建立磁碟區，您可以指定磁碟區，因為該磁碟區的固定在本機和主要資料不會分層式的 toohello 雲端。 本機固定磁碟區的快照集仍會複製 toohello 雲端備份，如此 hello 雲端可用於資料行動性和災害復原用途。 此外，您可以變更 hello 磁碟區類型 （也就是轉換分層磁碟區 toolocally 固定磁碟區和轉換在本機固定磁碟區 tootiered）。 
* **StorSimple 虛擬裝置改進**– 先前，hello StorSimple 8000 系列定位 hello 虛擬裝置做為災害復原或開發/測試方案。 只有一個虛擬裝置模型 (模型 1100)。 Update 2 導入兩個虛擬裝置模型： 
  
  * 8010 (先前稱為 hello 1100) – 不變更，容量為 30 TB，並使用標準的 Azure 儲存體。
  * 8020 – 具有 64 TB 的容量，並且使用 Azure 進階儲存體以改善效能。
    
    兩個虛擬裝置模型 (8010/8020) 有單一 VHD。 當您第一次啟動 hello 虛擬裝置時，它會偵測 hello 平台參數，並套用 hello 正確的模型版本。
* **網路功能改進**– Update 2 包含 hello 下列網路改進功能：
  
  * 以便處理能力的 NIC 失敗時進行容錯移轉，可以啟用多個 Nic hello 雲端。
  * 路由改進，具有已啟用雲端區塊的固定度量。
  * 在容錯移轉之前的失敗資源線上重試。
  * 服務失敗的新警示。
* **更新改進**– 在更新 1.2 和更早版本，從兩個通道傳送更新 hello StorSimple 8000 系列： 群集、 iSCSI 及等等及 Microsoft 二進位檔和韌體更新 Windows Update。
    Update 2 會針對所有更新套件使用 Microsoft Update。 這應該會導致 tooless 時間修補或進行容錯移轉。 
* **韌體更新**– hello 下列韌體更新會包含：
  
  * LSI：lsi_sas2.sys 產品版本 2.00.72.10
  * 只有 SSD (沒有 HDD 更新)：XMGG、XGEG、KZ50、F6C2 和 VR08
* **主動式支援**– Update 2 讓 Microsoft toopull 其他診斷資訊從裝置 hello。 當我們作業小組會識別發生問題的裝置時，我們會更好的配備的 toocollect 資訊從 hello 裝置，以及診斷問題。 **接受 Update 2 中，您允許我們 tooprovide 此主動式支援**。    

## <a name="issues-fixed-in-update-2"></a>在 Update 2 中修正的問題
hello 下表提供摘要的更新 2 中已修正的問題。    

| 否。 | 功能 | 問題 | 適用於 toophysical 裝置 | 適用於 toovirtual 裝置 |
| --- | --- | --- | --- | --- |
| 1 |網路介面 |升級 tooUpdate 1 之後, hello StorSimple Manager 服務所報告的 hello Data2 和 Data3 連接埠無法在一個控制器上。 已修正此問題。 |是 |否 |
| 2 |更新 |升級 tooUpdate 1 之後, 可發出聲音的警示通知中發生 hello 多個裝置上的 Azure 傳統入口網站。 已修正此問題。 |是 |否 |
| 3 |Openstack 驗證 |使用 Openstack 做為您的雲端服務提供者時，您可能會收到錯誤，表示您的雲端驗證字串過長。 已修正此問題。 |是 |否 |

## <a name="known-issues-in-update-2"></a>Update 2 中的已知問題
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
| 20 |固定在本機的磁碟區 |如果 tooconvert 分層磁碟區 （建立和複製與更新 1.2 或更早版本） 再試一次 tooa 本機固定磁碟區，而且您的裝置空間不足或在雲端中斷，則 hello clone(s) 可能會損毀。 |此問題只發生於使用 Update 2 之前的軟體所建立及複製的磁碟機。 這應該是不常見的案例。 | | |
| 21 |磁碟區轉換 |不會更新 hello Acr 附加的 tooa 磁碟區磁碟區轉換正在進行時 (釘選的分層式的 toolocally，反之亦然)。 更新 hello Acr，可能會導致資料損毀。 |如有需要更新 hello Acr 先前 toohello 磁碟區轉換並且不要讓任何進一步的 ACR 更新 hello 轉換正在進行時。 | | |

## <a name="controller-and-firmware-updates-in-update-2"></a>Update 2 中的控制器和韌體更新
這個版本會更新 hello 驅動程式和裝置上的 hello 磁碟韌體。

* 如需有關 hello LSI 韌體更新，請參閱 Microsoft 知識庫文章 3121900。 
* 如需有關 hello 磁碟韌體更新，請參閱 Microsoft 知識庫文章 3121899。

## <a name="virtual-device-updates-in-update-2"></a>Update 2 中的虛擬裝置更新
此更新無法套用的 toohello 虛擬裝置。 將新的虛擬裝置必須 toobe 建立。 

## <a name="next-step"></a>後續步驟
了解如何太[安裝 Update 2](storsimple-install-update-2.md) StorSimple 裝置上。

