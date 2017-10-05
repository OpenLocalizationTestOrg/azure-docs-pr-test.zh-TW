---
title: "StorSimple 8000 Update 0.2 版本資訊 | Microsoft Docs"
description: "說明 2015 年 1 月 Microsoft Azure StorSimple 版本 (Update 0.2) 的新功能與修正、未解決問題及可用的因應措施。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: d9684ae3-b38f-4678-9d70-e5dbc6b03350
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/16/2016
ms.author: v-sharos
ms.openlocfilehash: 2fc50f7faddb4b61ea5e7d328469fc3cc0eb6f3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="storsimple-8000-series-update-02-release-notes---january-2015"></a>StorSimple 8000 系列 Update 0.2 版本資訊 - 2015 年 1 月
## <a name="overview"></a>概觀
下列版本資訊指出 2015 年 1 月發行的 Microsoft Azure StorSimple 仍待解決的重要議題。 當中也包含此版本中隨附之 StorSimple 軟體與韌體更新的清單。 這是 StorSimple 8000 系列發行版本於 2014 年 7 月公開上市之後的第二個正式版本。

此更新並未變更 10 月更新的實體裝置軟體版本。 其依然是 6.3.9600.17312 版。 這個版本中由虛擬裝置影像使用的影像已經變更。 因此，2015/1/20 之後建立的所有新虛擬裝置都將顯示為 6.3.9600.17361 版。  

請檢閱版本資訊中包含的下列資訊，以取得 2015 年 1 月的更新。

> [!IMPORTANT]
> * 此更新無法透過 Windows Update 取得，安裝方式也和其他更新不一樣。 即使您透過 Azure 傳統入口網站套用此更新，您的裝置也不會收到更新。 此更新只會適用於 2015 年 1 月 20 日之後建立的虛擬裝置。 
> * 1 月發行的 StorSimple 不包含任何 StorSimple 實體裝置的更新。 您仍然可以將任何可用的 Windows 更新套用至虛擬裝置，包括近來的安全性修正程式，但不會改變 StorSimple 實體裝置的版本。
> 
> 

## <a name="whats-new-in-the-january-release"></a>1 月發行的新功能
此更新包含有關使虛擬裝置上的磁碟區離線的修正程式。 (請參閱 [此版本修正的問題](#issues-fixed-in-the-january-release))。  

此更新不包含新功能。  

## <a name="issues-fixed-in-the-january-release"></a>1 月版修正的問題
下表說明此更新已修正的問題。

| 編號 | 功能 | 問題 | 適用於實體裝置 | 適用於虛擬裝置 |
| --- | --- | --- | --- | --- |
| 1 |磁碟區離線 |當雲端延遲情況嚴重且長達數分鐘時，主機上的 StorSimple 虛擬裝置磁碟區就會離線。 此修正程式會增加雲端延遲的臨界值，如此可讓主機上的磁碟區變成離線的情況降至最低。 |否 |是 |

## <a name="known-issues-in-the-january-release"></a>1 月版已知的問題
下表提供此版本的已知問題摘要。

| 編號 | 功能 | 問題 | 註解/因應措施 | 適用於實體裝置 | 適用於虛擬裝置 |
| --- | --- | --- | --- | --- | --- |
| 1 |恢復出廠預設值 |在某些情況下，當您要恢復出廠預設值，StorSimple 裝置可能會卡住，並顯示此訊息：「正在重設為原廠預設值 (階段 8)」。 如果正在進行 Cmdlet 時，按 CTRL+C，就會發生這種情況。 |起始恢復出廠預設值後，請不要按 CTRL+C。 如果您已處於此狀態，請連絡 Microsoft 支援以進行後續步驟。 |是 |否 |
| 2 |磁碟仲裁 |在罕見情況下，如果 8600 裝置的 EBOD 機箱中大部分的磁碟都已中斷連線，而導致沒有磁碟仲裁，那麼將會使存放集區離線。 即使已重新連接磁碟時，它依然會保持離線。 |您必須重新啟動裝置。 如果問題持續發生， 請連絡 Microsoft 支援以進行後續步驟。 |是 |否 |
| 3 |雲端快照失敗 |在罕見情況下，雲端快照可能會失敗，發生「已達備份上限」 錯誤。 如果您在同一個裝置上已被刪除的同一個原始磁碟區有超過 255 個線上複本，就會發生這種情況。 | |是 |是 |
| 4 |不正確的控制器識別碼 |進行控制器更換時，控制器 0 可能顯示為控制器 1。 在控制器更換期間從對等節點載入影像時，控制器識別碼一開始可能會顯示為對等控制器的識別碼。  在罕見情況下，可能會在系統重新開機後出現這種行為。 |因此，使用者不需要採取任何動作。 控制器更換完成之後，會自行解決這種情況。 |是 |否 |
| 5 |裝置監控圖表 |在 StorSimple Manager 服務中，當裝置的 Proxy 伺服器組態中已啟用基本或 NTLM 驗證時，裝置監控圖表會沒有作用。 |請針對向 StorSimple Manager 服務註冊的裝置修改其 Web Proxy 組態設定，以便將驗證設定為 [無]。 若要這樣做，請執行 Windows PowerShell for StorSimple Set-HcsWebProxy Cmdlet。 |是 |是 |
| 6 |儲存體帳戶 |不支援使用儲存體服務刪除儲存體帳戶的案例。 這會導致無法擷取使用者資料的情況。 | |是 |是 |
| 7 |裝置容錯移轉 |不支援從相同來源裝置將某個磁碟區容器多次容錯移轉至不同的目標裝置。 |從單一失效裝置容錯移轉到多個裝置，會讓第一個容錯移轉裝置上的磁碟區容器失去資料擁有權。 進行這類容錯移轉之後，當您在 Azure 傳統入口網站中檢視這些磁碟區容器時，會發現它們的外觀或行為有所不同。 |是 |否 |
| 8 |安裝 |在 StorSimple Adapter for SharePoint 安裝其間，您必須提供裝置 IP，才能順利完成安裝。 | |是 |否 |
| 9 |Web Proxy |如果您的 Web Proxy 組態設定將 HTTPS 做為指定的通訊協定，您的裝置對服務通訊將會受到影響並使裝置離線。 同時會在程序中產生支援封裝，耗用裝置上的大量資源。 |請確定 Web Proxy URL 指定的通訊協定為 HTTP。 如需詳細資訊，請參閱如何 [設定裝置的 Web Proxy](storsimple-configure-web-proxy.md)。 |是 |否 |
| 10 |Web Proxy |如果您在註冊的裝置上設定並啟用 Web Proxy，將需要重新啟動裝置上的主動控制器。 | |是 |否 |
| 11 |雲端高延遲與高 I/O 工作負載 |當 StorSimple 裝置同時出現雲端延遲情況嚴重 (大約數秒) 和 I/O 工作負載高的情況時，裝置磁碟區會進入降級的狀態，而且 I/O 可能會失敗，發生「裝置未就緒」錯誤。 |您必須以手動方式將裝置控制器重新開機，或或執行裝置容錯移轉，才能從這種情況下復原。 |是 |否 |

## <a name="physical-device-updates-in-the-january-release"></a>1 月發行的實體裝置更新
此更新不包含任何其他 StorSimple 裝置的變更。

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-the-january-release"></a>1 月發行的序列連接 SCSI (SAS) 控制器與韌體更新
這個版本不包含任何序列連接 SCSI (SAS) 控制器或韌體的更新。 驅動程式更新已在 2014年 10 月發行。 

## <a name="virtual-device-updates-in-the-january-release"></a>1 月發行的虛擬裝置更新
此版本包含更新的虛擬裝置影像。 2015 年 1 月 20 日之後建立之所有虛擬裝置的軟體都將顯示為 6.3.9600.17361 版。

