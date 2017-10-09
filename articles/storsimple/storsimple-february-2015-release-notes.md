---
title: "aaaStorSimple 8000 更新 0.3 版本資訊 |Microsoft 文件"
description: "描述 hello 新功能和修正程式、 開啟問題，以及可用的因應措施 hello 2015 年 2 月 Microsoft Azure StorSimple 發行 （更新 0.3）。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: b01bfd04-f9f8-45f4-ade8-95ac2b979e6a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: 53638f9d286b2085c6b45f9e3fae75c34fc73e7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-03-release-notes---february-2015"></a>StorSimple 8000 系列 Update 0.3 版本資訊 - 2015 年 2 月
## <a name="overview"></a>概觀
下列版本資訊的 hello 識別 StorSimple 8000 系列 Update 0.3 2015 年 2 月發行 hello 重要的議題。 它們也包含一份 hello StorSimple 軟體和韌體更新這個版本中。 已在 2014 年 7 月正式推出 hello StorSimple 8000 系列版本的版本之後，這會是 hello 第三個版本。

此更新不會不變更 hello 年 1 月更新 hello 裝置軟體版本。 它會繼續 toobe 6.3.9600.17312 版。 您可以確認已安裝該 hello 更新檢查 hello**上次更新**日期。 如果 hello 日期為 2015 年 2 月 10 日或更新版本，然後 hello 更新已安裝成功。  

建議您在安裝 StorSimple 裝置後立即掃描並套用任何可用更新。 您也可以開啟自動更新 toodownload，並安裝來自 Microsoft 的高優先順序的更新，因為釋放它們。 如需詳細資訊，請參閱 [更新您的 StorSimple 裝置](storsimple-update-device.md)。  

請檢閱附註，然後再部署 hello 更新您的 StorSimple 解決方案中的 hello 版本中所包含的 hello 資訊。  

> [!IMPORTANT]
> * 使用 hello StorSimple Manager 服務和不要使用 Windows PowerShell for StorSimple tooinstall hello 2 月份更新。   
> * 它會採用大約小時 tooinstall 這項更新。 不過，如果您要安裝累計更新，hello 程序可能需要 3 小時 toocomplete。  
> * hello 年 2 月發行的 StorSimple 不包含任何更新 toohello StorSimple 虛擬裝置。 您仍然可以套用任何可用 Windows 更新 toohello 虛擬裝置，包括最近使用的安全性修正程式，但不是會看到 hello 虛擬裝置的版本中的變更。  
> 
> 

請確定該 hello 下列必要條件都符合先前 tooupdating StorSimple 裝置。  

* 在您掃描更新前，請確定這兩個裝置控制站都在執行中。 如果未執行兩個控制器，hello 掃描將會失敗。 tooverify hello 控制器處於狀況良好的狀態中，瀏覽過**硬體狀態**下 hello**維護**頁面。 如果有 [需要注意] 的元件，進一步繼續前，請連絡 Microsoft 支援。
* 請確定控制器 0 及控制器 1 固定的 Ip 可路由傳送，而且可連線 toohello 網際網路，因為這些用於服務 hello 更新 toohello 裝置。 您可以使用 hello [Test-connection cmdlet](https://technet.microsoft.com/library/hh849808.aspx) tooping hello 網路，例如 outlook.com，hello 控制站的 tooverify 之外的已知位址具有網路外部連線能力 toohello。
* 請確定 StorSimple 裝置上的連接埠 80 和 443 可用來進行傳出通訊。 如需詳細資訊，請參閱 hello [StorSimple 裝置的網路需求](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device)。
* Hello 裝置軟體版本早於 6.3.9600.17312 （2014 年 10 月更新） 時，停用 hello Data 2 和 Data 3 連接埠，如果啟用，再開始 hello 更新。 離開 hello 資料 2 或 3 通訊埠保持套用 hello 更新時可能會導致您的裝置控制器 toogo 進入修復模式。 請注意當您停用 hello 網路介面，hello 相關聯的所有磁碟區將會離線，且 hello I/o 將中斷 hello hello 更新期間。  

## <a name="whats-new-in-hello-february-release"></a>什麼是 hello 年 2 月版本的新功能
此更新包含在已經升級從 hello GA 版本 toohello 2014 年 10 月版本的裝置發生的 hello 原廠重設問題的修正。 如需詳細資訊，請參閱 [此版本修正的問題](#issues-fixed-in-the-february-release)。   

此更新不包含新功能。  

## <a name="issues-fixed-in-hello-february-release"></a>在 hello 年 2 月版本中修正的問題
hello 下表說明此更新中已修正的 hello 問題。  

| 否。 | 功能 | 問題 | 適用於 toophysical 裝置 | 適用於 toovirtual 裝置 |
| --- | --- | --- | --- | --- |
| 1 |恢復出廠預設值 |您嘗試的 tooperform 原廠重設最初 hello GA 版本 （6.3.9600.17215 版） 的裝置上安裝，但已更新的 toohello 年 10 月版本 （6.3.9600.17312 版）。 hello 原廠重設失敗和 hello 裝置變得不穩定。 |是 |否 |

## <a name="known-issues-in-hello-february-release"></a>Hello 年 2 月版本的已知的問題
hello 下表提供此版本已知問題的摘要。

| 否。 | 功能 | 問題 | 註解/因應措施 | 適用於 toophysical 裝置 | 適用於 toovirtual 裝置 |
| --- | --- | --- | --- | --- | --- |
| 1 |恢復出廠預設值 |在某些情況下，當您執行原廠重設 hello StorSimple 裝置可能當機並顯示下列訊息： **」 （階段 8） 正在執行重設 toofactory**。 會發生這種情況是如果正在進行 hello cmdlet 時，按 CTRL + C。 |起始恢復出廠預設值後，請不要按 CTRL+C。 如果您已處於此狀態，請連絡 Microsoft 支援以進行後續步驟。 |是 |否 |
| 2 |磁碟仲裁 |在罕見情況下，如果 hello 大多數的 8600device hello EBOD 機箱中的磁碟中斷連線，以致於沒有磁碟仲裁，則 hello 存放集區會離線。 即使 hello 磁碟重新連接會保持離線。 |您將需要 tooreboot hello 裝置。 如果 hello 問題持續發生，請連絡 Microsoft 支援以取得後續步驟。 |是 |否 |
| 3 |雲端快照失敗 |在罕見情況下，雲端快照可能失敗並 hello 錯誤**已達到備份上限**。 會發生這個錯誤超過 255 個線上複本，hello 上的相同的裝置 hello 從相同原始磁碟區已被刪除。 | |是 |是 |
| 4 |不正確的控制器識別碼 |進行控制器更換時，控制器 0 可能顯示為控制器 1。 控制器更換期間，從 hello 對等節點，載入 hello 映像時 hello 控制器識別碼最初可能顯示為 hello 同儕節點控制器的識別碼。 在罕見情況下，可能會在系統重新開機後出現這種行為。 |因此，使用者不需要採取任何動作。 Hello 控制器更換完成之後，這種情況下將自行解決。 |是 |否 |
| 5 |裝置監控圖表 |在 hello StorSimple Manager 服務，hello 裝置監控圖表不會運作時基本或 NTLM 驗證已啟用 hello 裝置 hello proxy 伺服器組態中。 |修改 hello 裝置向 StorSimple Manager 服務，讓驗證設定 tooNONE hello web proxy 的設定。 toodo，執行的 hello hello Windows PowerShell for StorSimple Set-hcswebproxy cmdlet。 |是 |是 |
| 6 |儲存體帳戶 |使用 hello 儲存體服務 toodelete hello 儲存體帳戶是不支援的案例。 這會導致無法擷取使用者資料所在的 tooa 情況。 | |是 |是 |
| 7 |裝置容錯移轉 |磁碟區容器從相同來源裝置 toodifferent 目標裝置不支援的 hello 的多個容錯移轉。    從單一失效裝置 toomultiple 裝置容錯移轉會使 hello 磁碟區容器上第一次容錯移轉裝置 hello 喪失資料擁有權。 這類容錯移轉之後，這些磁碟區容器將會出現，或當您在 hello Azure 傳統入口網站中檢視時有不同的行為。 | |是 |否 |
| 8 |安裝 |在 StorSimple Adapter for SharePoint 安裝，您必須 tooprovide 裝置 IP，為了讓 hello 安裝 toofinish 成功。 | |是 |否 |
| 9 |Web Proxy |如果您的 web proxy 組態已 HTTPS 做為 hello 指定通訊協定，則您裝置到服務的通訊會受到影響並且 hello 裝置會離線。 在 hello 過程中，使用您的裝置上的大量資源，也會產生支援封裝。 |請確定 hello web proxy URL 有 HTTP，如 hello 指定的通訊協定。 詳細資訊太[設定 web proxy 為您的裝置](storsimple-configure-web-proxy.md)。 |是 |否 |
| 10 |Web Proxy |如果您設定並啟用 web proxy 註冊的裝置上，您會在您的裝置上需要 toorestart hello 作用中控制器。 | |是 |否 |
| 11 |雲端高延遲與高 I/O 工作負載 |當您的 StorSimple 裝置發生極高雲端延遲 （秒數的順序） 和高 I/O 工作負載的組合時，hello 裝置磁碟區會進入降級狀態，而 hello I/o 可能會因 「 裝置未就緒 」 錯誤。 |您將會需要 toomanually 重新開機 hello 裝置控制器或執行裝置容錯移轉 toorecover 從這種情況。 |是 |否 |

## <a name="physical-device-updates-in-hello-february-release"></a>Hello 2 月版次中的實體裝置更新
此更新修正 hello 原廠重設在已經升級從 hello GA 版本 toohello 2014 年 10 月版本的裝置發生的問題。 它不包含任何其他更新 toohello StorSimple 裝置。  

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-february-release"></a>序列連結 SCSI (SAS) 控制器和韌體更新在 hello 年 2 月版本
此版本不包含任何更新 toohello 序列連結 SCSI (SAS) 控制器或韌體 hello。 hello 驅動程式更新已在 hello 年 10 月，2014年版本。  

## <a name="virtual-device-updates-in-hello-february-release"></a>Hello 2 月版次中的虛擬裝置更新
此版本不包含 hello 虛擬裝置的任何更新。 套用此更新不會變更虛擬裝置 hello 軟體版本。

