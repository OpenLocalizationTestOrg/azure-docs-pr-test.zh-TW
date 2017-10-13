---
title: "Azure Mobile Engagement 疑難排解指南 - 推送/觸達"
description: "Azure Mobile Engagement 中使用者互動與通知問題的疑難排解"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3f1886b7-1fdd-47f4-b6b0-d79f158d5ef3
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: ef6f34404b97a6972fc136262920a1bdbc4117b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-push-and-reach-issues"></a>推送與觸達問題的疑難排解指南
以下是您可能會遇到，有關 Azure Mobile Engagement 如何傳送資訊給使用者的問題。

## <a name="push-failures"></a>推送失敗
### <a name="issue"></a>問題
* 推送沒有運作 (在應用程式中、在應用程式外，或兩者)。

### <a name="causes"></a>原因
* 許多時候，推送失敗表示 Azure Mobile Engagement、Reach 或 Azure Mobile Engagement 的其他進階功能未正確整合，或是需要升級 SDK 以修正新的作業系統或裝置平台的已知問題。
* 測試應用程式內推送和應用程式外推送，以判斷這是應用程式內或應用程式外的問題。
* 同時從 UI 與 API 測試以做為疑難排解步驟，藉以查看這兩者中有哪些其他的錯誤資訊。
* 除非 SDK 中整合了 Azure Mobile Engagement 與 Reach，否則應用程式外推送不會運作。
* 如果憑證無效，或正在正確使用 PROD 與DEV 正確 (僅限 iOS)。 **注意**：如果您同時安裝開發版 (DEV) 和產品版 (PROD) 的應用程式在同一部裝置上，「應用程式外」推送將不會遞送給 iOS，因為與您憑證關聯的安全性權杖可能會由 Apple 作廢。 若要解決這個問題，請先解除安裝 DEV 和 PROD 版本的應用程式，然後在您的裝置上只安裝其中一個版本。)
* 應用程式外推送計數在不同的平台上有不同的處理方式 (如果裝置停用原生推送，iOS 顯示的資訊會比 Android 少，API 可以提供比 UI 更多的推送狀態相關資訊)。
* 應用程式外推送可以由客戶在作業系統層級 (iOS 與 Android) 封鎖。
* 如果應用程式外推送未正確整合，在 Azure Mobile Engagement UI 中會顯示為停用，但可能會從 API 以無訊息方式發生失敗。
* 除非 SDK 中同時整合了 Azure Mobile Engagement 與 Reach，否則應用程式內推送不會運作。
* 除非 SDK 中整合了 Azure Mobile Engagement 與特定伺服器，否則 GCM 與 ADM 推送不會運作 (僅限 Android)。
* 應用程式內推送和應用程式外推送應個別測試，以判斷是「推送」或「觸達」問題。
* 應用程式內推送要求應用程式開放被接收功能。
* 應用程式內推送通常設定為依據加入 (opt-in) 或退出 (opt-out) 應用程式資訊標記來篩選。
* 如果您在 Reach 中使用自訂類別來顯示應用程式內通知，您必須遵循通知的正確生命週期，否則當使用者關閉通知時可能不會清除通知。
* 如果您開始了一個沒有結束日期的活動，且裝置接收到應用程式內通知但尚未顯示，那麼即使您手動結束活動，使用者在下一次登入應用程式時仍然會收到通知。
* 對於推送 API 的問題，請確認您真的希望使用推送 API 而不是觸達 API (因為觸達 API 更常使用)，且您並沒有混淆 "payload" 和 "notifier" 參數。
* 使用透過 WIFI 與 3G 連線的裝置測試您的推播活動，來消除可能為問題來源的網路連線。

## <a name="push-testing"></a>推送測試
### <a name="issue"></a>問題
* 推送可以依據裝置識別碼傳送給特定的裝置。

### <a name="causes"></a>原因
* 測試裝置在各平台上有不同的設定，但是在您測試裝置上的應用程式中引發事件，以及在入口網站尋找您的裝置識別碼的功能應該運作，以尋找您的裝置在所有平台上的裝置識別碼。
* 測試裝置與 IDFA 與IDFV 搭配使用時運作方式不同 (僅 iOS)。

## <a name="push-customization"></a>自訂推送
### <a name="issue"></a>問題
* 進階推送內容項目無法運作 (徽章、響鈴、震動、圖片等)。
* 推送中的連結沒有作用 (應用程式外、應用程式內、網站連結、應用程式中的位置連結)。
* 推送統計資料顯示推送並沒有傳送給預期的人數 (太多或不足)。
* 重複推送，並且收到兩次。
* 無法為 Azure Mobile Engagement 推送註冊測試裝置 (使用您自己的 Prod 或 DEV 應用程式)。

### <a name="causes"></a>原因
* 要連結到應用程式內的特定位置時需要「類別」(僅限 Android)。
* 按一下推播通知後，重新導向使用者到替代位置的深層連結配置，必須由應用程式與裝置作業系統建立及管理，而非直接透過 Mobile Engagement。 (**注意**：應用程式外通知在 iOS 上無法像 Android 般，直接連結到應用程式位置。)
* 外部影像伺服器必須能夠使用 HTTP "GET" 與 "HEAD"，大型圖片推送才能運作 (僅限 Android)。
* 在您的程式碼中，您可以在鍵盤開啟時停用 Azure Mobile Engagement 代理程式，並讓程式碼在鍵盤關閉時重新啟用 Azure Mobile Engagement 代理程式，這樣一來鍵盤就不會影響您的通知的外觀 (僅限 iOS)。
* 部分項目在測試模擬中沒有作用，只有在實際活動 (徽章、響鈴、震動、圖片等) 中才會有作用。
* 當您使用按鈕「測試」推送時，不會記錄任何伺服器端的資料。 只會記錄實際推送活動的資料。
* 為了協助您找出問題，請以測試、模擬及實際活動來執行疑難排解，因為它們各自的運作方式稍有不同。
* 由於活動執行時，活動只會傳遞到「應用程式中」的使用者 (以及將裝置設定為接收「應用程式外」通知的使用者)，「應用程式中」與「任何時間」活動所安排執行的時間長度會影響傳遞的數目。
* Android 和 iOS 處理應用程式外通知方式的不同，導致難以直接比較應用程式 Android 和 iOS 版本兩者的推送統計數據。 Android 相較於 iOS，提供較多作業系統層級的通知資訊。 Android 在通知中心中接收、按一下、或是刪除原生通知時會報告，但 iOS 中除非按一下通知，否則不會報告此資訊，。 
* 觸達活動的「已推送」數目與「已傳遞」數目不同的主要原因，在於「應用程式中」與「應用程式外」的通知以不同的方式計算。 「應用程式中」通知由 Mobile Engagement 處理，但「應用程式外」通知則由裝置作業系統中的通知中心處理。

## <a name="push-targeting"></a>推送目標
### <a name="issue"></a>問題
* 內建目標未如預期般運作。
* 應用程式資訊標記目標未如預期般運作。
* 地理位置目標未如預期般運作。
* 語言選項未如預期般運作。

### <a name="causes"></a>原因
* 請確定您已經透過 Azure Mobile Engagement UI 或 API 上傳應用程式資訊標記。
* 於應用程式層級控制推送速度或推送配額，或於活動層級限制對象，可以防止使用者接收特定的推送，即使它們符合您其他的目標準則。 
* 設定「語言」和依據國家或地區設定目標不同，這也和依據地理位置、手機位置或 GPS 定位位置設定目標不同。
* 系統會傳送使用「預設語言」的訊息給未將其裝置設定為您所指定之替代語言之一的任何客戶。

## <a name="push-scheduling"></a>推送排程
### <a name="issue"></a>問題
* 推送排程未如預期般運作 (過早或延遲傳送)。

### <a name="causes"></a>原因
* 時區可能導致排程問題，特別是在使用使用者的時區時。
* 進階推送功能可能會延遲推送。
* 根據手機設定 (而不是根據應用程式資訊標記) 設定的目標可能會延遲推送，因為 Azure Mobile Engagement 可能必須在傳送推送之前，即時要求手機資料。
* 建立時未設定結束日期的活動會將推送儲存在本機裝置上，並在下一次應用程式開啟時顯示，即使活動已手動結束。
* 同時啟動多個活動可能需要較長時間來掃描您的使用者基礎 (請嘗試一次只啟動一個活動 (上限為四個)，目標也只限定於您在作用中的使用者，如此就不需要掃描舊的使用者)。
* 如果您在觸達活動的 [活動] 區段中使用 [略過對象，推送將透過 API 傳送給使用者] 選項，活動將不會自動傳送，您必須以手動方式透過「觸達 API」傳送活動。
* 如果您在 Reach 中使用自訂類別來顯示應用程式內通知，您必須遵循通知的正確生命週期，否則當使用者關閉通知時可能不會清除通知。

