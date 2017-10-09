---
title: "aaaStorSimple 8000 更新 0.2 版本資訊 |Microsoft 文件"
description: "描述 hello 新功能和修正程式、 開啟問題，以及可用的因應措施 hello 2015 年 1 月 （更新 0.2） 的 Microsoft Azure StorSimple 版本。"
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
ms.openlocfilehash: 1cee795df0b53d9b9276bc33074cf1a7aa188835
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-02-release-notes---january-2015"></a>StorSimple 8000 系列 Update 0.2 版本資訊 - 2015 年 1 月
## <a name="overview"></a>概觀
hello 下列版本資訊識別 hello 重大議題 hello 2015 年 1 月發行的 Microsoft Azure StorSimple。 它們也包含一份 hello StorSimple 軟體和韌體更新這個版本中。 已在 2014 年 7 月正式推出 hello StorSimple 8000 系列版本的版本之後，這會是 hello 第二個版本。

此更新不會不變更 hello 年 10 月更新 hello 實體裝置軟體版本。 它會繼續 toobe 6.3.9600.17312 版。 hello hello 虛擬裝置映像所使用的映像已在此版本中變更。 因此，所有 hello 新建立的虛擬裝置在 2015 年 1 月 20 日之後將 hello 版本都顯示為 6.3.9600.17361。  

請檢閱下列資訊包含在 hello hello 2015 年 1 月更新的版本資訊中的 hello。

> [!IMPORTANT]
> * 此更新無法透過 Windows Update 取得，安裝方式也和其他更新不一樣。 即使您已套用 hello 更新使用 hello Azure 傳統入口網站，您的裝置將不會收到這項更新。 此更新只會套用 toovirtual 2015 年 1 月 20 日之後建立的裝置。 
> * hello 年 1 月發行的 StorSimple 不包含任何更新 toohello StorSimple 實體裝置。 您仍然可以套用任何可用 Windows 更新 toohello 虛擬裝置，包括最近使用的安全性修正程式，但不是會看到 hello StorSimple 實體裝置的版本中的變更。
> 
> 

## <a name="whats-new-in-hello-january-release"></a>什麼是 hello 年 1 月版本的新功能
此更新包含修正相關 toohello hello 虛擬裝置上離線的磁碟區。 (請參閱 [此版本修正的問題](#issues-fixed-in-the-january-release))。  

hello 更新不包含新功能。  

## <a name="issues-fixed-in-hello-january-release"></a>在 hello 年 1 月版本中修正的問題
hello 下表說明此更新中已修正的 hello 問題。

| 否。 | 功能 | 問題 | 適用於 toophysical 裝置 | 適用於 toovirtual 裝置 |
| --- | --- | --- | --- | --- |
| 1 |磁碟區離線 |當高雲端延遲持續數分鐘時，hello StorSimple 虛擬裝置磁碟區離線 hello 主機上。 此修正程式會增加雲端延遲，因此降低 hello 情況下，會導致在主機上的離線 hello 磁碟區 toogo hello 臨界值。 |否 |是 |

## <a name="known-issues-in-hello-january-release"></a>Hello 年 1 月版本的已知的問題
hello 下表提供此版本已知問題的摘要。

| 否。 | 功能 | 問題 | 註解/因應措施 | 適用於 toophysical 裝置 | 適用於 toovirtual 裝置 |
| --- | --- | --- | --- | --- | --- |
| 1 |恢復出廠預設值 |在某些情況下，當您執行原廠重設 hello StorSimple 裝置可能當機並顯示下列訊息：**重設 toofactory 正在進行 （階段 8）。** 會發生這種情況是如果正在進行 hello cmdlet 時，按 CTRL + C。 |起始恢復出廠預設值後，請不要按 CTRL+C。 如果您已處於此狀態，請連絡 Microsoft 支援以進行後續步驟。 |是 |否 |
| 2 |磁碟仲裁 |在罕見情況下，如果 hello 大多數的 8600 裝置 hello EBOD 機箱中的磁碟中斷連線，以致於沒有磁碟仲裁，則 hello 存放集區會離線。 即使 hello 磁碟重新連接會保持離線。 |您將需要 tooreboot hello 裝置。 如果 hello 問題持續發生，請連絡 Microsoft 支援以取得後續步驟。 |是 |否 |
| 3 |雲端快照失敗 |在罕見情況下，雲端快照可能失敗並 hello 錯誤**已達到備份上限**。 會發生這個錯誤超過 255 個線上複本，hello 上的相同的裝置 hello 從相同原始磁碟區已被刪除。 | |是 |是 |
| 4 |不正確的控制器識別碼 |進行控制器更換時，控制器 0 可能顯示為控制器 1。 控制器更換期間，從 hello 對等節點，載入 hello 映像時 hello 控制器識別碼最初可能顯示為 hello 同儕節點控制器的識別碼。  在罕見情況下，可能會在系統重新開機後出現這種行為。 |因此，使用者不需要採取任何動作。 Hello 控制器更換完成之後，這種情況下將自行解決。 |是 |否 |
| 5 |裝置監控圖表 |在 hello StorSimple Manager 服務，hello 裝置監控圖表不會運作時基本或 NTLM 驗證已啟用 hello 裝置 hello proxy 伺服器組態中。 |修改 hello 裝置向 StorSimple Manager 服務，讓驗證設定 tooNONE hello web proxy 的設定。 toodo，執行的 hello hello Windows PowerShell for StorSimple Set-hcswebproxy cmdlet。 |是 |是 |
| 6 |儲存體帳戶 |使用 hello 儲存體服務 toodelete hello 儲存體帳戶是不支援的案例。 這會導致無法擷取使用者資料所在的 tooa 情況。 | |是 |是 |
| 7 |裝置容錯移轉 |磁碟區容器從相同來源裝置 toodifferent 目標裝置不支援的 hello 的多個容錯移轉。 |從單一失效裝置 toomultiple 裝置容錯移轉會使 hello 磁碟區容器上第一次容錯移轉裝置 hello 喪失資料擁有權。 這類容錯移轉之後，這些磁碟區容器將會出現，或當您在 hello Azure 傳統入口網站中檢視時有不同的行為。 |是 |否 |
| 8 |安裝 |在 StorSimple Adapter for SharePoint 安裝，您必須 tooprovide 裝置 IP，為了讓 hello 安裝 toofinish 成功。 | |是 |否 |
| 9 |Web Proxy |如果您的 web proxy 組態已 HTTPS 做為 hello 指定通訊協定，則您裝置到服務的通訊會受到影響並且 hello 裝置會離線。 在 hello 過程中，使用您的裝置上的大量資源，也會產生支援封裝。 |請確定 hello web proxy URL 有 HTTP，如 hello 指定的通訊協定。 如何查看詳細資訊，太[設定 web proxy 為您的裝置](storsimple-configure-web-proxy.md)。 |是 |否 |
| 10 |Web Proxy |如果您設定並啟用 web proxy 註冊的裝置上，您會在您的裝置上需要 toorestart hello 作用中控制器。 | |是 |否 |
| 11 |雲端高延遲與高 I/O 工作負載 |當您的 StorSimple 裝置發生極高雲端延遲 （秒數的順序） 和高 I/O 工作負載的組合時，hello 裝置磁碟區會進入降級狀態，而 hello I/o 可能會因 「 裝置未就緒 」 錯誤。 |您將會需要 toomanually 重新開機 hello 裝置控制器或執行裝置容錯移轉 toorecover 從這種情況。 |是 |否 |

## <a name="physical-device-updates-in-hello-january-release"></a>Hello 年 1 月版本中的實體裝置更新
此更新不包含任何其他變更 toohello StorSimple 裝置。

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-january-release"></a>序列連結 SCSI (SAS) 控制器和韌體更新在 hello 年 1 月版本
此版本不包含任何更新 toohello 序列連結 SCSI (SAS) 控制器或韌體 hello。 hello 驅動程式更新已在 hello 年 10 月，2014年版本。 

## <a name="virtual-device-updates-in-hello-january-release"></a>Hello 年 1 月版本中的虛擬裝置更新
這個版本包含更新的映像 hello 虛擬裝置。 2015 年 1 月 20 日之後建立的所有 hello 虛擬裝置會都顯示為 6.3.9600.17361 hello 軟體版本。

