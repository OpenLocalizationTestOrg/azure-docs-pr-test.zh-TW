---
title: "aaaAzure Mobile Engagement 疑難排解指南-服務"
description: "Azure Mobile Engagement 疑難排解"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8b4275da-c0b4-4690-824a-48e9d7a1fc6e
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: cf48db323a873ccef95946f7bb26e8d7473c002f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a>服務問題的疑難排解指南
hello 以下是可能的問題，您可能會遇到與 Azure Mobile Engagement 的執行方式。

## <a name="service-outages"></a>服務中斷
### <a name="issue"></a>問題
* 出現 toobe Azure Mobile Engagement 服務中斷所造成的問題。

### <a name="causes"></a>原因
* 出現 toobe Azure Mobile Engagement 服務中斷所造成的問題可能被因不同的幾個問題：
  * 原本出現的 Azure Mobile Engagement 全面 tooall 隔離的問題
  * 伺服器關閉所造成的已知問題 (不一定會顯示在伺服器狀態中)：
  * 排程延遲、 目標錯誤、 徽章更新問題、 統計資料停止收集，推入停止運作，應用程式開發介面的停止作用、 新的應用程式或使用者無法建立，DNS 錯誤及逾時錯誤裝置 hello UI、 API 或應用程式中。
  * 雲端相依性中斷 [Azure 服務狀態](http://status.azure.com/)
  * 推送通知服務 (PNS) 相依性中斷
  * 應用程式商店中斷

1) tootest toosee 全面 hello 問題時，您可以測試相同函式從不同的 hello

* Azure Mobile Engagement 整合式應用程式
* 測試裝置
* 測試裝置作業系統版本
* 活動
* 系統管理員使用者帳戶
* 瀏覽器 (IE、Firefox、Chrome 等)
* 電腦

2) 如果 hello 問題只會影響 hello UI 或 hello API，tootest:

* 測試相同的函式從這兩個 hello Azure Mobile Engagement UI 和 hello Azure Mobile Engagement 應用程式開發介面的 hello。

3) tootest hello 問題是否與您的行動電話網路：

* 測試連接 toohello 網際網路透過 WIFI 和時透過行動電話 3g 網路連線時。
* 確認您的防火牆不會封鎖任何 hello Azure Mobile Engagement IP 位址或連接埠。

4) tootest hello 問題是否與您的裝置：

* 測試您的裝置可以 tooconnect tooAzure Mobile Engagement 與另一個 Azure Mobile Engagement 整合式應用程式。
* 您可以從手機 hello Azure Mobile Engagement UI 中，可以看到產生的事件、 工作和當機的測試。 
* 測試您可以傳送推播通知從 hello Azure Mobile Engagement UI tooyour 裝置根據其裝置識別碼。 

5) tootest hello 問題是否與您的應用程式：

* 從模擬器 (而不是實體裝置)，安裝並測試您的應用程式：

6) tootest hello 問題是否與裝置，需要 SDK 升級 tooresolve OS 升級 tooend 使用者：

* 測試不同的裝置，具有不同版本的 hello OS 上的應用程式。
* 確認您使用的 hello hello SDK 最新版本。

## <a name="connectivity-and-incorrect-information-issues"></a>連線和資訊不正確的問題
### <a name="issue"></a>問題
* 登入問題 hello Azure Mobile Engagement UI。
* Hello Azure Mobile Engagement 應用程式開發介面的連接錯誤。
* 透過 hello 裝置 API 上傳應用程式資訊標記的問題。
* 從 Azure Mobile Engagement 下載記錄檔或匯出資料時發生問題。
* Hello Azure Mobile Engagement UI 中顯示的資訊不正確。
* Azure Mobile Engagement 記錄檔中顯示的資訊不正確。

### <a name="causes"></a>原因
* 請確認您的使用者帳戶有足夠的權限 tooperform hello 工作。
* 請確認該 hello 問題不是隔離的 tooone 電腦或區域網路。
* 請確認該 hello Azure Mobile Engagement 服務有任何回報的中斷。
* 確認您的應用程式資訊標記遵循以下所有規則：
  * 使用僅 hello UTF8 字元集 （不支援 hello ANSI 字元集）。
  * 使用逗號"，"hello 分隔符號字元 (您可以開啟 服務要求 toorequest toochange hello.csv 分隔符號字元逗號"，"tooanother 字元，例如分號";")。
  * 使用全部小寫的布林值 "true" 和 "false"。
  * 使用小於 hello 檔案大小上限為 35 MB 的檔案。

