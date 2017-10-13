---
title: "StorSimple 8000 Update 0.3 版本資訊 | Microsoft Docs"
description: "說明 2015 年 2 月 Microsoft Azure StorSimple 版本 (Update 0.3) 的新功能與修正、未解決問題及可用的因應措施。"
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
ms.openlocfilehash: c059fd74854813615754e67547497b7ededbe4dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="storsimple-8000-series-update-03-release-notes---february-2015"></a>StorSimple 8000 系列 Update 0.3 版本資訊 - 2015 年 2 月
## <a name="overview"></a>Overview
下列版本資訊指出 2015 年 2 月發行的 StorSimple 8000 系列 Update 0.3 版存有重大的未解決問題。 當中也包含此版本中隨附之 StorSimple 軟體與韌體更新的清單。 這是 StorSimple 8000 系列發行版本於 2014 年 7 月公開上市之後的第三個正式版本。

此更新並未變更 1 月更新的裝置軟體版本。 其依然是 6.3.9600.17312 版。 您可以檢查 [上次更新日期]  來確認已安裝的更新。 如果為 2015/2/10 或之後的日期，那麼就表示更新已安裝成功。  

建議您在安裝 StorSimple 裝置後立即掃描並套用任何可用更新。 您也可以開啟自動更新，以在 Microsoft 一發行高優先順序的更新時，便立即下載並安裝。 如需詳細資訊，請參閱＜ [更新您的 StorSimple 裝置](storsimple-update-device.md)＞。  

在 StorSimple 方案中部署更新之前，請檢閱版本資訊中所包含的資訊。  

> [!IMPORTANT]
> * 使用 StorSimple Manager 服務來安裝 2 月的更新，而非 Windows PowerShell for StorSimple。   
> * 安裝此更新，大約需要花費一小時。 不過，如果您要安裝累積更新，可能需要約 3 個小時才能完成程序。  
> * 2 月發行的 StorSimple 不包含任何 StorSimple 虛擬裝置的更新。 您仍然可以將任何可用的 Windows 更新套用至虛擬裝置，包括近來的安全性修正程式，但不會改變虛擬裝置的版本。  
> 
> 

更新 StorSimple 裝置前，請確定已符合下列必要條件。  

* 在您掃描更新前，請確定這兩個裝置控制站都在執行中。 如果有任一個控制器不在執行中，掃描就會失敗。 若要確認控制器處於狀況良好的狀態中，請瀏覽到 [維護] 頁面下的 [硬體狀態]。 如果有 [需要注意] 的元件，進一步繼續前，請連絡 Microsoft 支援。
* 請確定控制器 0 與控制器 1 兩者的固定 IP 都可路由，並可以連線到網際網路用來提供更新裝置的服務。 您可以使用 [測試連接 Cmdlet](https://technet.microsoft.com/library/hh849808.aspx) ，ping 網路外的已知位址，例如 outlook.com，以確認控制器有能力連線到外部網路。
* 請確定 StorSimple 裝置上的連接埠 80 和 443 可用來進行傳出通訊。 如需詳細資訊，請參閱 [StorSimple 裝置的網路需求](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device)。
* 如果裝置軟體比 6.3.9600.17312 版 (2014 年 10 月更新) 還舊，如果已啟用，請停用資料 2 與資料 3 連接埠後，再開始更新。 套用更新時，若讓資料 2 或資料 3 連接埠保持啟用狀態，可能會導致您的裝置控制站進入修復模式。 請注意，當您停用網路介面時，會使所有相關聯的磁碟區離線，並且會在更新期間中斷 I/O。  

## <a name="whats-new-in-the-february-release"></a>2 月發行的新功能
此更新已修正從 GA 版本升級至 2014 年 10  月版的裝置上所發生恢復出廠預設值的問題。 如需詳細資訊，請參閱 [此版本修正的問題](#issues-fixed-in-the-february-release)。   

此更新不包含新功能。  

## <a name="issues-fixed-in-the-february-release"></a>2 月版修正的問題
下表說明此更新已修正的問題。  

| 編號 | 功能 | 問題 | 適用於實體裝置 | 適用於虛擬裝置 |
| --- | --- | --- | --- | --- |
| 1 |恢復出廠預設值 |您在原本安裝 GA 版 (6.3.9600.17215 版) 但已更新至 10 月版 (6.3.9600.17312 版) 的裝置上，嘗試恢復出廠預設值。 恢復出廠預設值失敗，而且裝置變得不穩定。 |是 |否 |

## <a name="known-issues-in-the-february-release"></a>2 月版已知的問題
下表提供此版本的已知問題摘要。

| 編號 | 功能 | 問題 | 註解/因應措施 | 適用於實體裝置 | 適用於虛擬裝置 |
| --- | --- | --- | --- | --- | --- |
| 1 |恢復出廠預設值 |在某些情況下，當您要恢復出廠預設值，StorSimple 裝置可能會卡住，並顯示此訊息：「正在重設為原廠預設值 (階段 8)」 。 如果正在進行 Cmdlet 時，按 CTRL+C，就會發生這種情況。 |起始恢復出廠預設值後，請不要按 CTRL+C。 如果您已處於此狀態，請連絡 Microsoft 支援以進行後續步驟。 |是 |否 |
| 2 |磁碟仲裁 |在罕見情況下，如果 8600 裝置的 EBOD 機箱中大部分的磁碟都已中斷連線，而導致沒有磁碟仲裁，那麼將會使存放集區離線。 即使已重新連接磁碟時，它依然會保持離線。 |您必須重新啟動裝置。 如果問題持續發生， 請連絡 Microsoft 支援以進行後續步驟。 |是 |否 |
| 3 |雲端快照失敗 |在罕見情況下，雲端快照可能會失敗，發生「已達備份上限」 錯誤。 如果您在同一個裝置上已被刪除的同一個原始磁碟區有超過 255 個線上複本，就會發生這種情況。 | |是 |是 |
| 4 |不正確的控制器識別碼 |進行控制器更換時，控制器 0 可能顯示為控制器 1。 在控制器更換期間從對等節點載入影像時，控制器識別碼一開始可能會顯示為對等控制器的識別碼。 在罕見情況下，可能會在系統重新開機後出現這種行為。 |因此，使用者不需要採取任何動作。 控制器更換完成之後，會自行解決這種情況。 |是 |否 |
| 5 |裝置監控圖表 |在 StorSimple Manager 服務中，當裝置的 Proxy 伺服器組態中已啟用基本或 NTLM 驗證時，裝置監控圖表會沒有作用。 |請針對向 StorSimple Manager 服務註冊的裝置修改其 Web Proxy 組態設定，以便將驗證設定為 [無]。 若要這樣做，請執行 Windows PowerShell for StorSimple Set-HcsWebProxy Cmdlet。 |是 |是 |
| 6 |儲存體帳戶 |不支援使用儲存體服務刪除儲存體帳戶的案例。 這會導致無法擷取使用者資料的情況。 | |是 |是 |
| 7 |裝置容錯移轉 |不支援從相同來源裝置將某個磁碟區容器多次容錯移轉至不同的目標裝置。    從單一失效裝置容錯移轉到多個裝置，會讓第一個容錯移轉裝置上的磁碟區容器失去資料擁有權。 進行這類容錯移轉之後，當您在 Azure 傳統入口網站中檢視這些磁碟區容器時，會發現它們的外觀或行為有所不同。 | |是 |否 |
| 8 |安裝 |在 StorSimple Adapter for SharePoint 安裝其間，您必須提供裝置 IP，才能順利完成安裝。 | |是 |否 |
| 9 |Web Proxy |如果您的 Web Proxy 組態設定將 HTTPS 做為指定的通訊協定，您的裝置對服務通訊將會受到影響並使裝置離線。 同時會在程序中產生支援封裝，耗用裝置上的大量資源。 |請確定 Web Proxy URL 指定的通訊協定為 HTTP。 如需詳細資訊，請參閱如何 [設定裝置的 Web Proxy](storsimple-configure-web-proxy.md)。 |是 |否 |
| 10 |Web Proxy |如果您在註冊的裝置上設定並啟用 Web Proxy，將需要重新啟動裝置上的主動控制器。 | |是 |否 |
| 11 |雲端高延遲與高 I/O 工作負載 |當 StorSimple 裝置同時出現雲端延遲情況嚴重 (大約數秒) 和 I/O 工作負載高的情況時，裝置磁碟區會進入降級的狀態，而且 I/O 可能會失敗，發生「裝置未就緒」錯誤。 |您必須以手動方式將裝置控制器重新開機，或或執行裝置容錯移轉，才能從這種情況下復原。 |是 |否 |

## <a name="physical-device-updates-in-the-february-release"></a>2 月發行的實體裝置更新
此更新已修正從 GA 版本升級至 2014 年 10  月版的裝置上所發生恢復出廠預設值的問題。 它不包含任何其他 StorSimple 裝置的更新。  

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-the-february-release"></a>2 月發行的序列連接 SCSI (SAS) 控制器與韌體更新
這個版本不包含任何序列連接 SCSI (SAS) 控制器或韌體的更新。 驅動程式更新已在 2014年 10 月發行。  

## <a name="virtual-device-updates-in-the-february-release"></a>2 月發行的虛擬裝置更新
這個版本不包含任何虛擬裝置的更新。 套用此更新不會變更虛擬裝置的軟體版本。

