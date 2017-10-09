---
title: "aaaAzure Mobile Engagement 疑難排解指南-SDK"
description: "Azure Mobile Engagement 中 SDK 整合的疑難排解"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: de265cf1-2f88-43ef-8616-156ada5be7b6
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1c082b81d898f4bdb47b8efe6cfbacfd83fe9279
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a>SDK 整合問題的疑難排解指南
hello 以下是可能的問題，您可能會遇到與 Azure Mobile Engagement 如何整合到應用程式。

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a>因為您應用程式的另一個區域中發生失敗而發現的 SDK 問題
### <a name="issue"></a>問題
* UI 資料收集失敗 (在分析、監視、分割或儀表板中)。
* 推送失敗 (推送在應用程式內或應用程式外無法運作，或在兩個情況下都無法運作)。
* 進階功能失敗 (追蹤、地理位置或平台特定的推送無法運作)。
* API 失敗 (API 經常以無訊息模式失敗，沒有錯誤訊息)。
* 服務失敗 (所有 Azure Mobile Engagement 都無法在您的應用程式上運作)。

### <a name="causes"></a>原因
* 大部分需要 toobe 解決 hello Azure Mobile Engagement SDK 的問題將會探索您的應用程式 （例如 UI 資料收集失敗、 推入失敗、 進階的功能失敗、 應用程式開發介面失敗、 應用程式損毀或明顯服務失敗中斷的狀況）。  
* 如果特定功能的 Azure Mobile Engagement 具有永遠不會在您的應用程式之前，您需要 toocomplete hello 整合。 
* 如果 Azure Mobile Engagement 的特定功能運作，而停止，您可能需要以 hello Azure Mobile Engagement SDK tooupgrade toohello 最後一個版本。 請記住每個平台支援的 Azure Mobile Engagement （Android、 iOS、 Windows 和 Windows Phone） hello Azure Mobile Engagement SDK 不同版本。

#### <a name="sdk-integration"></a>SDK 整合
* Azure Mobile Engagement 未正確整合在 SDK 中 (分析)。
* Reach 未正確整合在 SDK 中 (應用程式內推送和應用程式外推送)。
* 憑證已過期或 PROD 與 DEV 不正確 (僅限 iOS)。
* GCM 或 ADM 未正確整合在 SDK 中 (僅限 Android - 服務特定推送)。
* 追蹤未正確整合在 SDK 中 (安裝存放區追蹤)。
* 延遲位置或 GPS 位置未正確整合在 SDK 中 (依地理位置設定目標)。

**另請參閱：**

* [SDK 文件 - 整合指南][Link 5] 
* [疑難排解指南 - 推送][Link 23]

#### <a name="sdk-upgrade"></a>SDK 升級
* 需要 tooupgrade SDK tooresolve 問題與舊版本的 hello SDK （通常相關的 toonewer hello 裝置作業系統版本）。
* 從您的裝置解除安裝所有舊版的應用程式，並重新安裝應用程式的 hello 最新版本，hello 重新註冊您的裝置識別碼，從您的裝置正在使用您的應用程式的 hello 最新版本的 hello Azure Mobile Engagement UI tooconfirm。

**另請參閱：**

* [SDK 文件 - 版本資訊](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [SDK 文件 - 升級指南](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a>SDK 其他問題
* 在應用程式資訊清單"AndroidManifest.xml 」 的錯誤可能會導致 Azure Mobile Engagement toowork (僅 Android)。
* 常見的問題與 SDK 整合及應用程式開發介面使用方式為 tooconfuse hello SDK 金鑰和 hello API 金鑰。

**另請參閱：**

* [概念 - 詞彙][Link 6]

## <a name="advanced-coding-issues"></a>進階編碼問題
### <a name="issue"></a>問題
* 平台特定程式碼不是直接相關的 tooAzure Mobile Engagement 進行 iOS、 Android 和 Windows Phone，可能會導致某些問題。

### <a name="causes"></a>原因
* 有許多進階與 Azure Mobile Engagement 的撰寫問題的原因藉由撰寫不正確的平台特定程式碼不是直接相關的 tooAzure Mobile Engagement。 您將需要 tooconsult 文件特定 toohello 平台您正在開發此外 tooAzure Mobile Engagement 文件 （Android、 iOS、 Web、 Windows 和 Windows Phone）。
* 未正確設定 「 類別 」，可避免從內部或外部 hello 應用程式 (僅 Android) 的通知 tooanother 位置連結。 
* 未設定太 「 選用 」 在您的 iOS 程式碼，便會顯示 「 找不到錯誤的符號""UIKit.framework 」 及 （或較舊的 iOS 裝置 (僅限 iOS) 上發生當機)。
* 過期的憑證或未正確使用 hello 開發人員或生產環境版本 hello cert，原因發送問題 (僅限 iOS)。
* 有一些限制固有 tooa 平台的 Azure Mobile Engagement 無法控制 （例如如何 hello system center 的運作方式的應用程式外推播通知在 Android 和 iOS）。
* Azure Mobile Engagement 發行參考使用的 Azure Mobile Engagement 適用於 iOS 和 Android 的 hello 內部套件的完整清單。 請記住，某些功能的 Azure Mobile Engagement 是特定 toohello 平台 （Android、 iOS、 Web、 Windows 和 Windows Phone）。

### <a name="see-also"></a>另請參閱
* [疑難排解指南 - 推送][Link 23] 
* [SDK 文件 - 版本資訊][Link 5]
* [SDK 文件 - 升級指南][Link 5]

## <a name="application-crashes"></a>應用程式當機
### <a name="issue"></a>問題
* 應用程式損毀 hello 結束使用者的裝置上。

### <a name="causes"></a>原因
* 可以在 hello 檢視損毀資訊*分析 UI*或 hello*分析 API*
* 您可以找到 hello 測試裝置的裝置識別碼，並採取 hello 相同的動作，導致您的應用程式 toocrash 的終端使用者 toohelp 識別 hello 程式損毀原因。
* 以 hello Azure Mobile Engagement SDK 的已知的問題會造成應用程式 toocrash 有時被解決方法是升級 toohello hello SDK 最新版本。 調查損毀時，請確定您的平台有關 toocheck hello 版本資訊。

### <a name="see-also"></a>另請參閱
* [SDK 文件 - 版本資訊][Link 5]
* [SDK 文件 - 升級指南][Link 5]

## <a name="app-store-upload-failures"></a>應用程式商店上傳失敗
### <a name="issue"></a>問題
* 錯誤相關的應用程式 tooApple、 Google、 或 hello Windows 應用程式存放區的 toouploading hello 最新版本。

### <a name="causes"></a>原因
* 應用程式會將有時封鎖應用程式已啟用特定功能 （例如 hello Apple Store 防止 IDFV 的 hello 存放區中的應用程式中的 hello 利用並 hello GooglePlay 存放區可防止 hello 共用應用程式之間的應用程式資訊）。 
* 請確定您檢查 hello 版本資訊有關您的平台和目前 hello SDK 版本，如果您無法上傳應用程式 toohello 市集。

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

