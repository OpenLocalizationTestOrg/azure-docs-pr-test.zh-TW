---
title: "aaaStorSimple 8000 發行版本的版本資訊 |Microsoft 文件"
description: "描述 hello 新功能、 開啟問題，以及可用的因應措施 hello 2014 年 7 月發行 Microsoft Azure StorSimple。"
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
ms.openlocfilehash: 74863a3e2811dc7be5e6f482a5be4bbc37e3cd71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-release-version-release-notes---july-2014"></a>StorSimple 8000 系列發行版本的版本資訊 - 2014 年 7 月
## <a name="overview"></a>概觀
hello 後續版本資訊識別 hello 重大議題 hello StorSimple 8000 系列的 Microsoft Azure StorSimple 2014 年 7 月的公開上市 (GA) 版本。 這個版本對應 toosoftware 版本 6.3.9600.17215。  

除非另行指定，這些版本資訊適用於 tooall hello StorSimple 裝置的模型。 hello 版本資訊會持續更新;發現需要因應措施的重大問題時，會加入。 在您部署 Microsoft Azure StorSimple 方案之前，請考量下列資訊的 hello。  

## <a name="known-issues-in-this-release"></a>此版本已知的問題
hello 下表提供此版本已知問題的摘要。  

| 否。 | 功能 | 問題 | 註解/因應措施 | 適用於 toophysical 裝置 | 適用於 toovirtual 裝置 |
| --- | --- | --- | --- | --- | --- |
| 1 |恢復出廠預設值 |在某些情況下，當您執行原廠重設 hello StorSimple 裝置可能當機並顯示下列訊息： **」 （階段 8） 正在執行重設 toofactory**。 會發生這種情況是如果正在進行 hello cmdlet 時，按 CTRL + C。 |起始恢復出廠預設值後，請不要按 CTRL+C。 如果您已處於此狀態，請連絡 Microsoft 支援以進行後續步驟。 |是 |否 |
| 2 |磁碟仲裁 |在罕見情況下，如果 hello 大多數的 8600 裝置 hello EBOD 機箱中的磁碟中斷連線，以致於沒有磁碟仲裁，則 hello 存放集區會離線。 即使 hello 磁碟重新連接會保持離線。 |您將需要 tooreboot hello 裝置。 如果 hello 問題持續發生，請連絡 Microsoft 支援以取得後續步驟。 |是 |否 |
| 3 |雲端快照失敗 |在罕見情況下，雲端快照可能失敗並 hello 錯誤**已達到備份上限**。 會發生這個錯誤超過 255 個線上複本，hello 上的相同的裝置 hello 從相同原始磁碟區已被刪除。 | |是 |是 |
| 4 |不正確的控制器識別碼 |進行控制器更換時，控制器 0 可能顯示為控制器 1。 控制器更換期間，從 hello 對等節點，載入 hello 映像時 hello 控制器識別碼最初可能顯示為 hello 同儕節點控制器的識別碼。 在罕見情況下，可能會在系統重新開機後出現這種行為。 |因此，使用者不需要採取任何動作。 Hello 控制器更換完成之後，這種情況下將自行解決。 |是 |否 |
| 5 |裝置監控圖表 |在 hello StorSimple Manager 服務，hello 裝置監控圖表不會運作時基本或 NTLM 驗證已啟用 hello 裝置 hello proxy 伺服器組態中。 |修改 hello 裝置向 StorSimple Manager 服務，讓驗證設定 tooNONE hello web proxy 的設定。 toodo，執行的 hello hello Windows PowerShell for StorSimple Set-hcswebproxy cmdlet。 |是 |是 |
| 6 |儲存體帳戶 |使用 hello 儲存體服務 toodelete hello 儲存體帳戶是不支援的案例。 這會導致無法擷取使用者資料所在的 tooa 情況。 | |是 |是 |
| 7 |容錯回復 |災害復原 (DR) 不支援 24 小時內容錯回復。 | |是 |否 |
| 8 |裝置容錯移轉 |磁碟區容器從相同來源裝置 toodifferent 目標裝置不支援的 hello 的多個容錯移轉。 從單一失效裝置 toomultiple 裝置容錯移轉會使 hello 磁碟區容器上第一次容錯移轉裝置 hello 喪失資料擁有權。 這類容錯移轉之後，這些磁碟區容器將會出現，或當您在 hello Azure 傳統入口網站中檢視時有不同的行為。 | |是 |否 |
| 9 |安裝 |在 StorSimple Adapter for SharePoint 安裝，您需要 tooprovide 裝置 IP hello 安裝 toofinish 成功。 | |是 |否 |
| 10 |網路介面 |Hello 軟體中，已交換網路介面 DATA 2 和 DATA 3。 |請如果您需要 tooconfigure 這些介面，連絡 Microsoft 支援。 |是 |否 |

