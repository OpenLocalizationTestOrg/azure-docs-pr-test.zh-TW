---
title: "aaaStorSimple 8000 更新 0.1 版本資訊 |Microsoft 文件"
description: "描述 hello 新功能和修正程式、 開啟問題，以及可用的因應措施 hello 2014 年 10 月 Microsoft Azure StorSimple 發行 （更新 0.1）。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: fd35e3c3-4770-460c-999d-f72ab7053a20
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 684e31cb0b356ec59a9d6c245e5d2bc062cc4f0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-01-release-notes--october-2014"></a>StorSimple 8000 系列 Update 0.1 版本資訊 – 2014 年 10 月
## <a name="overview"></a>概觀
下列版本資訊的 hello 識別 StorSimple 8000 系列 Update 0.1 於 2014 年 10 月發行 hello 重要的議題。 它們也包含一份 hello StorSimple 軟體和韌體更新這個版本中。 已在 2014 年 7 月正式推出 hello StorSimple 8000 系列版本的版本，並對應 toosoftware 6.3.9600.17312 版之後，這會是 hello 第一個版本。  

我們建議您掃描，並安裝 hello 裝置之後，立即套用任何可用的更新。 您也可以開啟自動更新 toodownload，並安裝來自 Microsoft 的高優先順序的更新，因為釋放它們。 如需詳細資訊，請參閱如何太[更新您的 StorSimple 裝置](storsimple-update-device.md)。  

請檢閱 hello hello 更新部署在您於 StorSimple 解決方案之前先 hello 版本資訊中所包含的資訊。  

> [!IMPORTANT]
> * 使用 hello StorSimple Manager 服務和不要使用 Windows PowerShell for StorSimple tooinstall hello 年 10 月更新。  
> * hello 更新通常需要大約 3 小時 toocomplete。  
> * hello 年 10 月發行的 StorSimple 不包含任何更新 toohello StorSimple 虛擬裝置。 您仍然可以套用任何可用 Windows 更新，包括最新的安全性修正程式，但將不會看到 hello 虛擬裝置的版本中的變更。  
> 
> 

請確定 hello 下列必要條件都符合先前 tooupdating StorSimple 裝置。  

* 在您掃描更新前，請確定這兩個裝置控制站都在執行中。 如果未執行兩個控制器，hello 掃描將會失敗。 tooverify hello 控制器處於狀況良好的狀態中，瀏覽過**硬體狀態**下 hello**維護**頁面。 如果有 [需要注意] 的元件，進一步繼續前，請連絡 Microsoft 支援。  
* 請確定控制器 0 固定的 Ip 及控制器 1 可路由傳送，而且可連線 toohello 網際網路，因為這些用於服務 hello 更新 toohello 裝置。 您可以使用 hello [Test-connection cmdlet](https://technet.microsoft.com/library/hh849808.aspx) tooping （如 outlook.com)，hello 控制站的 tooverify hello 網路之外的已知位址具有網路外部連線能力 toohello。  
* 請確定該 hello 所需的輸出連接埠的連出通訊您 StorSimple 裝置上的可用。 如需詳細資訊，請參閱 hello [StorSimple 裝置的網路需求](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device)。  
* Hello 裝置軟體版本早於 6.3.9600.17312 （2014 年 10 月更新） 時，停用 hello Data 2 和 Data 3 連接埠，如果啟用，再開始 hello 更新。 如果您離開 hello 資料 2 或 3 通訊埠保持套用 hello 更新時，它會導致您的裝置控制器 toogo 進入修復模式。 請注意當您停用 hello 網路介面，hello 相關聯的所有磁碟區將會離線，且 hello I/O 將中斷 hello hello 更新期間。  

## <a name="whats-new-in-hello-october-release"></a>什麼是 hello 年 10 月版本的新功能
此更新包含下列增強功能的 hello:

* 您現在可以使用 hello StorSimple Manager 服務 UI toomanage 您的裝置控制器。 hello 管理動作包括重新啟動、 關機，或開啟控制器。 如需詳細資訊，請移至太[管理 StorSimple 裝置控制器](storsimple-manage-device-controller.md)。  
* 您可以排程 WAN 頻寬配置，根據的週 tooday 和當天時間的組合。 這可讓您 toomake 更妥善運用 WAN 頻寬在離峰時間。 不同的磁碟區容器允許使用不同的頻寬範本。 如需詳細資訊，請移至太[管理您的 StorSimple 頻寬範本](storsimple-manage-bandwidth-templates.md)。  
* 您可以設定電子郵件通知 tooproactively 通知 hello 給系統管理員和其他現有或可能產生問題。 如需詳細資訊，請移至太[設定警示設定](storsimple-manage-alerts.md#configure-alert-settings)。  

## <a name="issues-fixed-in-hello-october-release"></a>在 hello 年 10 月版本中修正的問題
hello 下表提供此更新中已修正的問題摘要。  

| 否。 | 功能 | 問題 | 適用於 toophysical 裝置 | 適用於 toovirtual 裝置 |
| --- | --- | --- | --- | --- |
| 1 |網路介面 |在先前的 hello 釋放、 hello 軟體中已交換 hello 網路介面 DATA 2 和 DATA 3。 此更新已經修正這個問題。 請清除 hello 設定，並停用這些網路介面，才能安裝 hello 更新。 在安裝之後 hello 更新，您必須 tooreconfigure 這些介面。 |是 |否 |
| 2 |支援封裝 |在 hello 先前版本中，如果您執行 Windows PowerShell hello **Export-hcssupportpackage** cmdlet tooretrieve hello 基礎板管理控制器 (BMC) 記錄，hello 作業失敗，發生 hello 下列警告:"hello作業在此控制站，成功，但因為 toohello 下列 hello 同儕節點控制器上失敗的錯誤。 請檢查是否狀況良好 hello 對等與 hello 目前節點是否可連接 toohello 對等。 」 」 現已修正此問題。 |是 |否 |
| 3 |裝置容錯移轉 |在 hello 先前版本中，時可能發生資料不一致。 如果**探索備份**工作在裝置容錯移轉期間失敗。 」 現已修正此問題。 |是 |否 |
| 4 |裝置容錯移轉 |在先前的 hello 釋放、 裝置容錯移轉之後，備份可以看見，但 hello 相關聯的磁碟區容器不存在於 hello 目標裝置上。 」 現已修正此問題。 |是 |否 |
| 5 |裝置容錯移轉 |在 hello 先前版本中，有已 hello 列舉型別中的雲端備份如果沒有雲端連線問題可能會導致 toodata 不一致的 hello 登錄還原作業期間的 bug。 |是 |否 |
| 6 |韌體更新 |在 hello 舊版 hello 裝置韌體更新工作失敗，並顯示 hello 因 cmdlet 無法辨識，，和該 hello 更新而導致失敗的錯誤。 hello 控制器接著進入修復模式。 」 現已修正此問題。 |是 |否 |
| 7 |安裝 |在安裝期間未正確處理 hello 裝置所造成的錯誤現在已獲得修正。 |是 |否 |
| 8 |恢復出廠預設值 |您可以現在選擇性地略過原廠重設的 hello 韌體檢查。 這是來自 hello 前一版的變更。 |是 |否 |
| 9 |恢復出廠預設值 |在 hello 先前版本中，當原廠重設 cmdlet 執行時，版本進行韌體檢查只會針對某些硬體元件。 這會使得 hello 重設 toofail hello 程序中的 hello 第一次重新開機後進行額外的韌體檢查。 此修正可確保所有 hello 韌體檢查都都會 hello 原廠重設 cmdlet 執行並且之前 hello 第一次系統重新開機。 |是 |否 |
| 10 |替換儲存體帳戶金鑰 |hello **Invoke-hcsmservicedataencryptionkeychange** cmdlet 現在提示 hello 使用者 tooenter hello 服務資料加密金鑰，請使用 toorotate hello 儲存體帳戶金鑰。 這是從服務資料加密金鑰傳遞做為內嵌參數中的 hello hello 舊版的變更。 |是 |否 |
| 11 |24 小時內容錯回復 |嚴重損壞修復期間 hello 清除 hello 來源裝置上的並未發生完全，因而導致容錯回復 toofail。 此版本已經修正這個問題。 |是 |否 |

## <a name="known-issues-in-hello-october-release"></a>Hello 年 10 月版本的已知的問題
hello 下表提供此版本已知問題的摘要。

| 否。 | 功能 | 問題 | 註解/因應措施 | 適用於 toophysical 裝置 | 適用於 toovirtual 裝置 |
| --- | --- | --- | --- | --- | --- |
| 1 |恢復出廠預設值 |在某些情況下，當您執行原廠重設 hello StorSimple 裝置可能當機並顯示下列訊息： **」 （階段 8） 正在執行重設 toofactory**。 會發生這種情況是如果正在進行 hello cmdlet 時，按 CTRL + C。 |起始恢復出廠預設值後，請不要按 CTRL+C。 如果您已處於此狀態，請連絡 Microsoft 支援以進行後續步驟。 |是 |否 |
| 2 |恢復出廠預設值 |執行原廠重設更新從 GA tooOctober 2014 版本的 StorSimple 裝置。 |只有安裝修補程式後，這項操作才能運作。 請連絡 Microsoft 支援服務 tooget 這個必要的修補程式。 |是 |否 |
| 3 |磁碟仲裁 |在罕見情況下，如果 hello 大多數的 8600 裝置 hello EBOD 機箱中的磁碟中斷連線，以致於沒有磁碟仲裁，則 hello 存放集區會離線。 即使 hello 磁碟重新連接會保持離線。 |您將需要 tooreboot hello 裝置。 如果 hello 問題持續發生，請連絡 Microsoft 支援以取得後續步驟。 |是 |否 |
| 4 |雲端快照失敗 |在罕見情況下，雲端快照可能失敗並 hello 錯誤**已達到備份上限**。 會發生這個錯誤超過 255 個線上複本，hello 上的相同的裝置 hello 從相同原始磁碟區已被刪除。 | |是 |是 |
| 5 |不正確的控制器識別碼 |進行控制器更換時，控制器 0 可能顯示為控制器 1。 控制器更換期間，從 hello 對等節點，載入 hello 映像時 hello 控制器識別碼最初可能顯示為 hello 同儕節點控制器的識別碼。 在罕見情況下，可能會在系統重新開機後出現這種行為。 |因此，使用者不需要採取任何動作。 Hello 控制器更換完成之後，這種情況下將自行解決。 |是 |否 |
| 6 |裝置監控圖表 |在 hello StorSimple Manager 服務，hello 裝置監控圖表不會運作時基本或 NTLM 驗證已啟用 hello 裝置 hello proxy 伺服器組態中。 |修改 hello 裝置向 StorSimple Manager 服務，讓驗證設定 tooNONE hello web proxy 的設定。 toodo，執行的 hello hello Windows PowerShell for StorSimple Set-hcswebproxy cmdlet。 |是 |是 |
| 7 |儲存體帳戶 |使用 hello 儲存體服務 toodelete hello 儲存體帳戶是不支援的案例。 這會導致無法擷取使用者資料所在的 tooa 情況。 | |是 |是 |
| 8 |裝置容錯移轉 |磁碟區容器從相同來源裝置 toodifferent 目標裝置不支援的 hello 的多個容錯移轉。 |從單一失效裝置 toomultiple 裝置容錯移轉會使 hello 磁碟區容器上第一次容錯移轉裝置 hello 喪失資料擁有權。 這類容錯移轉之後，這些磁碟區容器將會出現，或當您在 hello Azure 傳統入口網站中檢視時有不同的行為。 |是 |否 |
| 9 |安裝 |在 StorSimple Adapter for SharePoint 安裝，您必須 tooprovide 裝置 IP，為了讓 hello 安裝 toofinish 成功。 | |是 |否 |
| 10 |Web Proxy |如果您的 web proxy 組態已 HTTPS 做為 hello 指定通訊協定，則您裝置到服務的通訊會受到影響並且 hello 裝置會離線。 在 hello 過程中，使用您的裝置上的大量資源，也會產生支援封裝。 |請確定 hello web proxy URL 有 HTTP，如 hello 指定的通訊協定。 詳細資訊太[設定 web proxy 為您的裝置](storsimple-configure-web-proxy.md)。 |是 |否 |
| 11 |Web Proxy |如果您設定並啟用 web proxy 註冊的裝置上，您會在您的裝置上需要 toorestart hello 作用中控制器。 | |是 |否 |
| 12 |雲端高延遲與高 I/O 工作負載 |當您的 StorSimple 裝置發生極高雲端延遲 （秒數的順序） 和高 I/O 工作負載的組合時，hello 裝置磁碟區會進入降級狀態，而 hello I/o 可能會因 「 裝置未就緒 」 錯誤。 |您將會需要 toomanually 重新開機 hello 裝置控制器或執行裝置容錯移轉 toorecover 從這種情況。 |是 |否 |

## <a name="physical-device-updates-in-hello-october-release"></a>Hello 年 10 月版本中的實體裝置更新
當這些更新套用的 tooa 實體裝置，hello 軟體版本會變更 too6.3.9600.17312。 除非另行指定，這些版本資訊適用於 tooall hello StorSimple 裝置的模型。 如需有關這些更新的詳細資訊，請參閱 [2014 年 10 月 Microsoft Azure StorSimple 應用裝置的實體應用裝置軟體更新](http://support.microsoft.com/kb/2986997)。  

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-october-release"></a>序列連結 SCSI (SAS) 控制器和韌體更新在 hello 年 10 月版本
這個版本會更新 hello 驅動程式與您的實體裝置 hello SAS 控制器上的 hello 韌體。 如需 hello SAS 控制器更新的詳細資訊，請參閱[2014 年 10 月更新的 Microsoft Azure StorSimple 應用裝置中的 LSI SAS 控制器](http://support.microsoft.com/kb/2987020)。   

此版本也套用了累計韌體更新，解決 hello 裝置硬體元件的可靠性問題。 如需 hello 韌體更新的詳細資訊，請參閱[Microsoft Azure StorSimple 應用裝置 2014 年 10 月韌體更新](http://support.microsoft.com/kb/2987015)。  

## <a name="virtual-device-updates-in-hello-october-release"></a>Hello 年 10 月版本中的虛擬裝置更新
此版本不包含 hello 虛擬裝置的任何更新。 套用此更新不會變更虛擬裝置 hello 軟體版本。

