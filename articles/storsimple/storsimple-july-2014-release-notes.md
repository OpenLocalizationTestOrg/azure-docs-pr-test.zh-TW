---
title: "StorSimple 8000 發行版本的版本資訊 | Microsoft Docs"
description: "說明 2014 年 7 月 Microsoft Azure StorSimple 版本的新功能、未解決問題及可用的因應措施。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 12f1796e-37c3-42b4-b997-a84fc1950c20
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: 303cdffa15fdfe9b83d0612edecafc6943d218f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="storsimple-8000-series-release-version-release-notes---july-2014"></a>StorSimple 8000 系列發行版本的版本資訊 - 2014 年 7 月
## <a name="overview"></a>概觀
下列版本資訊指出 2014 年 7 月發行的 StorSimple 8000 系列 Microsoft Azure StorSimple 公開上市 (GA) 版存在重大的未解決問題。 這個版本會對應到軟體版本 6.3.9600.17215。  

除非另有指定，否則這些版本資訊適用於所有 StorSimple 裝置模型。 版本資訊會持續更新。每當發現需要提出因應措施的重大問題時都會有所增補。 在部署 Microsoft Azure StorSimple 方案之前，請考慮下列資訊。  

## <a name="known-issues-in-this-release"></a>此版本已知的問題
下表提供此版本的已知問題摘要。  

| 編號 | 功能 | 問題 | 註解/因應措施 | 適用於實體裝置 | 適用於虛擬裝置 |
| --- | --- | --- | --- | --- | --- |
| 1 |恢復出廠預設值 |在某些情況下，當您要恢復出廠預設值，StorSimple 裝置可能會卡住，並顯示此訊息：「正在重設為原廠預設值 (階段 8)」 。 如果正在進行 Cmdlet 時，按 CTRL+C，就會發生這種情況。 |起始恢復出廠預設值後，請不要按 CTRL+C。 如果您已處於此狀態，請連絡 Microsoft 支援以進行後續步驟。 |是 |否 |
| 2 |磁碟仲裁 |在罕見情況下，如果 8600 裝置的 EBOD 機箱中大部分的磁碟都已中斷連線，而導致沒有磁碟仲裁，那麼將會使存放集區離線。 即使已重新連接磁碟時，它依然會保持離線。 |您必須重新啟動裝置。 如果問題持續發生， 請連絡 Microsoft 支援以進行後續步驟。 |是 |否 |
| 3 |雲端快照失敗 |在罕見情況下，雲端快照可能會失敗，發生「已達備份上限」 錯誤。 如果您在同一個裝置上已被刪除的同一個原始磁碟區有超過 255 個線上複本，就會發生這種情況。 | |是 |是 |
| 4 |不正確的控制器識別碼 |進行控制器更換時，控制器 0 可能顯示為控制器 1。 在控制器更換期間從對等節點載入影像時，控制器識別碼一開始可能會顯示為對等控制器的識別碼。 在罕見情況下，可能會在系統重新開機後出現這種行為。 |因此，使用者不需要採取任何動作。 控制器更換完成之後，會自行解決這種情況。 |是 |否 |
| 5 |裝置監控圖表 |在 StorSimple Manager 服務中，當裝置的 Proxy 伺服器組態中已啟用基本或 NTLM 驗證時，裝置監控圖表會沒有作用。 |請針對向 StorSimple Manager 服務註冊的裝置修改其 Web Proxy 組態設定，以便將驗證設定為 [無]。 若要這樣做，請執行 Windows PowerShell for StorSimple Set-HcsWebProxy Cmdlet。 |是 |是 |
| 6 |儲存體帳戶 |不支援使用儲存體服務刪除儲存體帳戶的案例。 這會導致無法擷取使用者資料的情況。 | |是 |是 |
| 7 |容錯回復 |災害復原 (DR) 不支援 24 小時內容錯回復。 | |是 |否 |
| 8 |裝置容錯移轉 |不支援從相同來源裝置將某個磁碟區容器多次容錯移轉至不同的目標裝置。 從單一失效裝置容錯移轉到多個裝置，會讓第一個容錯移轉裝置上的磁碟區容器失去資料擁有權。 進行這類容錯移轉之後，當您在 Azure 傳統入口網站中檢視這些磁碟區容器時，會發現它們的外觀或行為有所不同。 | |是 |否 |
| 9 |安裝 |在 StorSimple Adapter for SharePoint 安裝其間，您必須提供裝置 IP，以供順利完成安裝。 | |是 |否 |
| 10 |網路介面 |軟體中會交換網路介面 DATA 2 與 DATA 3。 |如果您需要設定這些介面，請連絡 Microsoft 支援。 |是 |否 |

