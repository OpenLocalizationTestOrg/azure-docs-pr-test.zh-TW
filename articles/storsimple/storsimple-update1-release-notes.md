---
title: "aaaStorSimple 8000 系列 Update 1.2 版本資訊 |Microsoft 文件"
description: "StorSimple 8000 系列 Update 1.2 描述 hello 新功能、 問題和因應措施。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6c9aae87-6f77-44b8-b7fa-ebbdc9d8517c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7f564b794573fc3302ab15732e8dd85632ab9243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="update-12-release-notes-for-your-storsimple-8000-series-device"></a>StorSimple 8000 系列裝置的 Update 1.2 版本資訊

## <a name="overview"></a>概觀
hello 下列版本資訊說明 hello 新功能和識別 hello 重大議題 StorSimple 8000 系列 Update 1.2。 它們也包含一份 hello StorSimple 軟體、 驅動程式的這一版中所包含的磁碟韌體更新。 

更新 1.2 可以執行版本 (GA)、 更新 0.1、 0.2，更新或更新 0.3 軟體的套用的 tooany StorSimple 裝置。 如果您的裝置是執行 Update 1 或 Update 1.1，就無法使用 Update 1.2。 如果您的裝置正在執行版本 (GA)，請[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)tooassist 您安裝此更新。

下列表格列出 hello 裝置軟體版本對應 tooUpdates 1、 1.1 和 1.2 hello。

| 如果執行更新... | 這是您裝置的軟體版本。 |
| --- | --- |
| Update 1.2 |6.3.9600.17584 |
| Update 1.1 |6.3.9600.17521 |
| Update 1.0 |6.3.9600.17491 |

請檢閱附註，然後再部署 hello 更新您的 StorSimple 解決方案中的 hello 版本中所包含的 hello 資訊。 如需詳細資訊，請參閱如何太[StorSimple 裝置上安裝更新 1.2](storsimple-install-update-1.md)。 

> [!IMPORTANT]
> * 它會採用大約 5-10 小時 tooinstall 這項更新 （包括 hello Windows 更新）。 
> * Update 1.2 具有軟體、LSI 驅動程式和磁碟韌體更新。 tooinstall，遵循中的 hello 指示[StorSimple 裝置上安裝更新 1.2](storsimple-install-update-1.md)。
> * 新的版本，您可能不會看到更新立即，因為我們會執行 hello 更新分階段導入。 請在數天內再次掃描更新，因為很快就會提供更新。
> 
> 

## <a name="whats-new-in-update-12"></a>Update 1.2 的新功能
使用 Update 1 所提出的可用 tooa 有限的一組使用者第一次發行這些功能。 Hello 更新 1.2 版本中，大部分的 hello StorSimple 使用者會看到下列新功能和增強功能的 hello:

* **從 5000 7000 系列 too8000 系列裝置的移轉**– 此版本導入了新的移轉功能，可讓 hello StorSimple 5000 7000 系列裝置使用者 toomigrate 其資料 tooa StorSimple 8000 系列實體裝置或虛擬應用裝置。 hello 移轉功能具有兩個重要價值主張：                                                                  
  
  * **業務續航力**，進而 5000 7000 系列裝置 too8000 數列應用裝置上的現有資料移轉。
  * **改善的 hello 8000 系列裝置的供應項目功能**，例如有效率的多個裝置透過 StorSimple Manager 服務的集中式管理、 更佳的硬體類別，並且更新韌體、 虛擬應用裝置、 資料行動力，與 hello 未來藍圖中的功能。
    
    請參閱 toohello[移轉指南](http://www.microsoft.com/download/details.aspx?id=47322)的詳細資料 toomigrate StorSimple 5000 7000 系列 tooan 8000 系列裝置。 
* **Hello Azure 政府入口網站中的可用性**– StorSimple 現已推出 hello Azure 政府入口網站。 請參閱如何太[部署 StorSimple 裝置 hello Azure 政府入口網站中的](storsimple-deployment-walkthrough-gov.md)。
* **其他雲端服務提供者支援**– hello 支援其他雲端服務提供者會 Amazon S3 Amazon S3 RR、 HP、 與 OpenStack (beta)。
* **更新儲存體 Api toolatest** – StorSimple 人已經與此版本中，更新 toohello 最新 Azure 儲存體服務 Api。 StorSimple 8000 系列裝置正在執行且在 Update 1 軟體版本 (版本中，0.1、 0.2 和 0.3) 使用 hello 早於 2009 年 7 月 17 日的 Azure 儲存體服務 Api 的版本。 Hello 更新中所述[移除儲存體服務版本的相關公告](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx)，這些 Api 會被取代的 2016 年 8 月 1 日。 請務必您套用 hello StorSimple 8000 系列 Update 1 之前 tooAugust 1、 2016年。 如果您讓容錯 toodo，StorSimple 裝置將會停止運作正常。
* **支援的區域備援儲存體 (ZRS)** – hello StorSimple 8000 系列 hello 升級 toohello 最新版本 hello 儲存體 Api，將會支援區域備援儲存體 (ZRS)，在加法 tooLocally 備援儲存體 (LRS) 」 和 「 地理備援儲存體 (GRS)。 參考 toothis [Azure 儲存體備援選項上的文章](../storage/common/storage-redundancy.md)如 ZRS 詳細資料。
* **增強初始的部署和更新體驗**– 在此版本中，hello 安裝並更新處理程序中已有所強化。 hello 安裝精靈的 hello 安裝是改善的 tooprovide 意見反應 toohello 使用者 hello 網路設定和防火牆設定不正確。 已提供其他診斷 cmdlet toohelp 您進行疑難排解的 hello 裝置的網路功能。 請參閱 hello[疑難排解部署文章](storsimple-troubleshoot-deployment.md)如需有關新 hello 做為疑難排解的診斷 cmdlet。

## <a name="issues-fixed-in-update-12"></a>在 Update 1.2 中修正的問題
hello 下表提供摘要的 1.2、 1.1 及 1 的更新中已修正的問題。    

| 否。 | 功能 | 問題 | 在 Update 中修正的問題 | 適用於 toophysical 裝置 | 適用於 toovirtual 裝置 |
| --- | --- | --- | --- | --- | --- |
| 1 |Windows PowerShell for StorSimple |當使用者從遠端使用 Windows PowerShell for StorSimple 中存取 hello StorSimple 裝置，然後啟動 hello 安裝精靈盡 Data 0 IP 已輸入發生當機。 這個 Bug 現在已在 Update 1 中修正。 |Update 1 |是 |是 |
| 2 |恢復出廠預設值 |在某些情況下，當您執行原廠重設 hello StorSimple 裝置變成當機並顯示此訊息： **」 （階段 8） 正在執行重設 toofactory**。 發生此錯誤是如果正在進行中的 hello cmdlet 時，按下 CTRL + C。 這個 Bug 現在已修正。 |Update 1 |是 |否 |
| 3 |恢復出廠預設值 |失敗的雙重控制器原廠重設之後，您允許 tooproceed 使用裝置註冊。 這會產生不支援的系統組態。 在 Update 1 中，會顯示錯誤訊息，而且在恢復出廠預設值失敗的裝置上，會阻止進行註冊。 |Update 1 |是 |否 |
| 4 |恢復出廠預設值 |在某些情況下，會引發誤判的不相符警示。 在執行 Update 1 的裝置上，將不會再產生不正確的不相符警示。 |Update 1 |是 |否 |
| 5 |恢復出廠預設值 |如果原廠重設執行已中斷，先前的 toocompletion hello 裝置進入修復模式，而且不允許您 tooaccess Windows PowerShell for StorSimple。 這個 Bug 現在已修正。 |Update 1 |是 |否 |
| 6 |災害復原 |災害復原 (DR) bug 的修正其中 DR 將會失敗期間 hello 探索 hello 目標裝置上的備份。 |Update 1 |是 |是 |
| 7 |監控 LED |在某些情況下，在 hello 應用裝置的背面監控 Led 未指出正確的狀態。 hello 藍色 LED 已關閉。 即使在未設定這些介面時，DATA 0 和 DATA 1 LED 也在閃爍。 已修正 hello 問題，並監控 Led 現在會指出 hello 正確的狀態。 |Update 1 |是 |否 |
| 8 |監控 LED |在某些情況下，套用 Update 1 後 hello 作用中控制器上的藍色 hello light 關閉便成為硬 tooidentify hello 作用中控制器。 此修補程式版本已修正此問題。 |Update 1.2 |是 |否 |
| 9 |網路介面 |在舊版中，使用無法路由的閘道設定的 StorSimple 裝置可能會離線。 在此版本中，data 0 的 hello 路由公制發出 hello 最低;因此，即使其他網路介面具備雲端功能，透過 Data 0 將會路由所有來自 hello 裝置 hello 雲端流量。 |Update 1 |是 |是 |
| 10 |備份 |在 hello 修補程式修正 24 天後造成備份 toofail Update 1 中的錯誤釋放更新 1.1。 |Update 1.1 |是 |是 |
| 11 |備份 |舊版中的錯誤導致雲端快照集變更率低，且效能不佳。 此修補程式版本已修正此問題。 |Update 1.2 |是 |是 |
| 12 |更新 |中，報告升級失敗，並進入修復模式，導致 hello 控制器 toogo Update 1 的 bug 已修正此修補程式版本。 |Update 1.2 |是 |是 |

## <a name="known-issues-in-update-12"></a>Update 1.2 中的已知問題
hello 下表提供此版本已知問題的摘要。

| 否。 | 功能 | 問題 | 註解/因應措施 | 適用於 toophysical 裝置 | 適用於 toovirtual 裝置 |
| --- | --- | --- | --- | --- | --- |
| 1 |磁碟仲裁 |在罕見情況下，如果 hello 大多數的 8600 裝置 hello EBOD 機箱中的磁碟中斷連線，以致於沒有磁碟仲裁，則 hello 存放集區會離線。 即使 hello 磁碟重新連接會保持離線。 |您將需要 tooreboot hello 裝置。 如果 hello 問題持續發生，請連絡 Microsoft 支援以取得後續步驟。 |是 |否 |
| 2 |不正確的控制器識別碼 |進行控制器更換時，控制器 0 可能顯示為控制器 1。 控制器更換期間，從 hello 對等節點，載入 hello 映像時 hello 控制器識別碼最初可能顯示為 hello 同儕節點控制器的識別碼。 在罕見情況下，可能會在系統重新開機後出現這種行為。 |因此，使用者不需要採取任何動作。 Hello 控制器更換完成之後，這種情況下將自行解決。 |是 |否 |
| 3 |儲存體帳戶 |使用 hello 儲存體服務 toodelete hello 儲存體帳戶是不支援的案例。 這會導致無法擷取使用者資料所在的 tooa 情況。 |是 |是 | |
| 4 |裝置容錯移轉 |磁碟區容器從相同來源裝置 toodifferent 目標裝置不支援的 hello 的多個容錯移轉。 從單一失效裝置 toomultiple 裝置的裝置容錯移轉會使 hello 磁碟區容器上第一次容錯移轉裝置 hello 喪失資料擁有權。 這類容錯移轉之後，這些磁碟區容器將會出現，或當您在 hello Azure 傳統入口網站中檢視時有不同的行為。 | |是 |否 |
| 5 |安裝 |在 StorSimple Adapter for SharePoint 安裝，您必須 tooprovide 裝置 IP，為了讓 hello 安裝 toofinish 成功。 | |是 |否 |
| 6 |Web Proxy |如果您的 web proxy 組態已 HTTPS 做為 hello 指定通訊協定，則您裝置到服務的通訊會受到影響並且 hello 裝置會離線。 在 hello 過程中，使用您的裝置上的大量資源，也會產生支援封裝。 |請確定 hello web proxy URL 有 HTTP，如 hello 指定的通訊協定。 如需詳細資訊，請移至太[設定 web proxy 為您的裝置](storsimple-configure-web-proxy.md)。 |是 |否 |
| 7 |Web Proxy |如果您設定並啟用 web proxy 註冊的裝置上，您會在您的裝置上需要 toorestart hello 作用中控制器。 | |是 |否 |
| 8 |雲端高延遲與高 I/O 工作負載 |當您的 StorSimple 裝置發生極高雲端延遲 （秒數的順序） 和高 I/O 工作負載的組合時，hello 裝置磁碟區會進入降級狀態，而 hello I/o 可能會因 「 裝置未就緒 」 錯誤。 |您將會需要 toomanually 重新開機 hello 裝置控制器或執行裝置容錯移轉 toorecover 從這種情況。 |是 |否 |
| 9 |Azure PowerShell |當您使用 hello StorSimple cmdlet **Get AzureStorSimpleStorageAccountCredential &#124;Select-object-先 1-等候**tooselect hello 第一個物件，好讓您可以建立新**磁碟區容器**物件 hello cmdlet 會傳回所有的 hello 物件。 |將 hello cmdlet 包裝在括號，如下所示： **(Get-Azure-StorSimpleStorageAccountCredential) &#124;Select-object-先 1-等候** |是 |是 |
| 10 |移轉 |移轉傳遞多個磁碟區容器，hello 知道最新備份時，只為第一個磁碟區容器 hello 精確。 此外，hello hello 第一個磁碟區容器中的前 4 個備份移轉之後，會進行平行的移轉。 |建議您一次移轉一個磁碟區容器。 |是 |否 |
| 11 |移轉 |Hello 還原之後，磁碟區不會新增 toohello 備份原則或 hello 虛擬磁碟群組。 |您將需要 tooadd 順序 toocreate 備份這些磁碟區 tooa 備份原則。 |是 |是 |
| 12 |移轉 |Hello 移轉完成之後，hello 5000/7000 系列裝置不得存取 hello 移轉資料容器。 |我們建議您刪除 hello hello 移轉便會完成認可之後，移轉資料容器。 |是 |否 |
| 13 |複製和 DR |執行 Update 1 的 StorSimple 裝置無法複製或執行嚴重損壞修復 tooa 裝置執行更新前 1 軟體。 |您將需要 tooupdate hello 目標裝置 tooUpdate 1 tooallow 這些作業 |是 |是 |
| 14 |移轉 |當磁碟區群組中沒有相關聯的磁碟區時，5000-7000 系列裝置上用於移轉的設定備份可能會失敗。 |刪除所有 hello 空的磁碟區群組與沒有相關聯的磁碟區，然後再重試 hello 設定備份。 |是 |否 |

## <a name="physical-device-updates-in-update-12"></a>Update 1.2 中的實體裝置更新
如果套用的 tooa 實體裝置 （執行版本先前 tooUpdate 1） 修補程式更新 1.2，hello 軟體版本會變更 too6.3.9600.17584。

## <a name="controller-and-firmware-updates-in-update-12"></a>Update 1.2 中的控制器和韌體更新
這個版本會更新 hello 驅動程式和裝置上的 hello 磁碟韌體。

* 如需 hello SAS 控制器更新的詳細資訊，請參閱[Update 1 的 Microsoft Azure StorSimple 應用裝置中的 LSI SAS 控制器](https://support.microsoft.com/kb/3043005)。 
* 如需 hello 磁碟韌體更新的詳細資訊，請參閱[Microsoft Azure StorSimple 應用裝置磁碟韌體更新 1](https://support.microsoft.com/kb/3063416)。

## <a name="virtual-device-updates-in-update-12"></a>Update 1.2 中的虛擬裝置更新
此更新無法套用的 toohello 虛擬裝置。 將新的虛擬裝置必須 toobe 建立。 

## <a name="next-steps"></a>後續步驟
* [在您的裝置上安裝 Update 1.2](storsimple-install-update-1.md)。

