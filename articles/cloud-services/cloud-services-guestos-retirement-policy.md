---
title: "Azure 客體作業系統的 aaaSupportability 和淘汰原則指南 |Microsoft 文件"
description: "提供 Microsoft 將會支援 as regards toohello 雲端服務所使用的 Azure 客體作業系統的相關資訊。"
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 919dd781-4dc6-4e50-bda8-9632966c5458
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/26/2017
ms.author: raiye
ms.openlocfilehash: 6a86c42ac95d12bbf116d900b7afb26fc3fe34e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-guest-os-supportability-and-retirement-policy"></a>Azure 客體作業系統可支援性和淘汰原則
此頁面上的 hello 資訊與相關 toohello Azure 客體作業系統 ([客體 OS](cloud-services-guestos-update-matrix.md)) 的雲端服務背景工作角色和 web 角色 (PaaS)。 它不會套用 tooVirtual 機器 (IaaS)。

Microsoft 有已發行[hello 客體作業系統的支援原則](http://support.microsoft.com/gp/azure-cloud-lifecycle-faq)。 您正在閱讀的 hello 頁面現在會描述 hello 原則的實作方式。

hello 原則

1. Microsoft 將會支援**至少 hello hello 客體作業系統的最新的兩個系列**。 當某個系列淘汰時，客戶會有 12 個月的 hello 正式淘汰日期 tooupdate tooa 較新且支援客體 OS 系列的時間。
2. Microsoft 將會支援**至少 hello hello 支援客體 OS 系列的最新的兩個版本**。
3. Microsoft 將會支援**至少 hello 的 hello Azure SDK 最新的兩個版本**。 當 hello 淘汰 SDK 的版本時，客戶將會有 12 個月的 hello 正式淘汰日期 tooupdate tooa 較新版本的時間。

Microsoft 有時候會支援兩個以上的系列或版本。 正式客體 OS 支援資訊將會出現在 hello [Azure 客體 OS 版本與 SDK 相容性比較表](cloud-services-guestos-update-matrix.md)。

## <a name="when-a-guest-os-family-or-version-is-retired"></a>當客體作業系統系列或版本遭到淘汰時
新的客體 OS**系列**一段時間以後 hello 官方新版 hello Windows 伺服器作業系統的版本。 每當引進新的客體作業系統系列，Microsoft 將會淘汰 hello 最舊的客體 OS 系列。

新的客體 OS**版本**大約為每個月 tooincorporate hello 最新的 MSRC 更新引進。 Hello 每月定期更新，因為客體 OS 版本是通常停用其發行後的 60 天。 此活動會保持每個系列至少有兩個客體 OS 版本可供使用。

### <a name="process-during-a-guest-os-family-retirement"></a>客體作業系統系列淘汰期間的程序
一旦公告 hello 淘汰，客戶有 12 個月 「 過渡 」 期之前 hello 舊的系列正式從服務中移除。 此轉換的時間可能會擴充的 Microsoft hello 斟酌。 更新會公佈於 hello [Azure 客體 OS 版本與 SDK 相容性比較表](cloud-services-guestos-update-matrix.md)。

漸進的淘汰程序會將六個 （6） 個月開始到 hello 過渡期。 在這段時間：

1. Microsoft 將通知客戶 hello 淘汰。
2. hello 較新版本的 hello Azure SDK 將不會支援 hello 淘汰客體 OS 系列。
3. 新的部署和雲端服務的使用不允許 hello 淘汰的系列上

Microsoft 將持續 toointroduce 新的客體 OS 版本之前 hello hello 過渡期，又稱為 hello 「 過期日 」 的最後一天中納入 hello 最新的 MSRC 更新。 上 hello 到期日，仍在執行的雲端服務，會依據 hello Azure SLA 不再受支援。 Microsoft 有 hello 自行斟酌 tooforce 升級、 刪除或停止這些服務在讓日期之後。

### <a name="process-during-a-guest-os-version-retirement"></a>客體作業系統版本淘汰期間的程序
如果客戶設定其 tooautomatically 客體 OS 的更新，就不需要 tooworry 有關客體 OS 版本處理。 他們會一律使用最新客體 OS 版本 hello。

Microsoft 會在每個月發行客體作業系統。 由於定期發行的 hello 頻率，每個版本都有固定的使用期限。

版本是經過 hello 使用期限的 60 天，「*停用*"。 「 停用 」 表示該 hello 版本會移除從 hello 入口網站。 hello 版本不再可以設定從 hello CSCFG 組態檔中。 現有部署仍可繼續執行。 但是，新的部署和程式碼和組態的更新 tooexisting 部署將不允許。

段時間後變得 「 停用 「 hello 客體 OS 版本 」*到期*"和仍在執行該版本的任何安裝都將遭到強制升級，並設定 hello 的 tooautomatically 更新 hello 客體作業系統未來。 到期日是所以批次中的停用 tooexpiration hello 期間可能會不同。

這些期間可能會進行長在 Microsoft 的自行斟酌 tooease 客戶轉換。 任何變更將會傳送 hello 上[Azure 客體 OS 版本與 SDK 相容性比較表](cloud-services-guestos-update-matrix.md)。

### <a name="notifications-during-retirement"></a>淘汰期間的通知
* **系列淘汰** <br>Microsoft 會透過部落格文章和入口網站通知公告。 透過直接通訊 （電子郵件、 入口網站訊息、 撥打電話） tooassigned 服務系統管理員，系統會通知仍在使用已淘汰的客體 OS 系列的客戶。 所有變更都將都張貼 toothis 頁面和 hello RSS 摘要列於此頁面的 hello 開頭。
* **版本淘汰** <br>所有變更與 hello 日期發生時將會都公佈 toothis 頁面和 hello RSS 摘要的這個頁面上，包括發行、 已停用和到期 hello 開頭所列出。 如果遭停用的客體作業系統版本或系列之上仍有運作中的部署，服務管理員將會收到電子郵件。 這些電子郵件的 hello 時間而有所不同。 雖然發送電子郵件的時間不屬於官方 SLA，不過 Microsoft 通常會在停用之前至少一個月發出。

## <a name="frequently-asked-questions"></a>常見問題集
**我要如何降低移轉的 hello 影響？**

建議您使用最新的客體 OS 系列來設計雲端服務。

1. 啟動及早規劃您移轉 tooa 較新的系列。
2. 設定暫時測試部署 tootest hello 新的系列上執行的雲端服務。
3. 設定您的客體 OS 版本太**自動**(osVersion = * 在 hello [.cscfg](cloud-services-model-and-package.md#cscfg)檔案) 讓 hello 移轉 toonew 客體 OS 版本會自動發生。

**如果我的 web 應用程式需要與 hello OS 的更深入整合？**

如果您的 web 應用程式架構相依於基礎 hello 作業系統功能，使用支援的平台功能例如[啟動工作](cloud-services-startup-tasks.md)或其他擴充性機制。 或者，您也可以使用[Azure 虛擬機器](https://azure.microsoft.com/documentation/scenarios/virtual-machines/)(IaaS-基礎結構即服務)，您必須負責維護基礎作業系統的 hello。

## <a name="next-steps"></a>後續步驟
最新檢閱 hello[客體 OS 版本](cloud-services-guestos-update-matrix.md)。
