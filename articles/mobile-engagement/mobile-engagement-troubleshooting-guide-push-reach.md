---
title: "aaaAzure Mobile Engagement 疑難排解指南-推入/觸達"
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
ms.openlocfilehash: 4ee0b34b9b753a98ccf24863acb28a5dc76bfb95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-push-and-reach-issues"></a>推送與觸達問題的疑難排解指南
hello 以下是可能的問題，您可能會遇到與 Azure Mobile Engagement 傳送資訊 tooyour 使用者的方式。

## <a name="push-failures"></a>推送失敗
### <a name="issue"></a>問題
* 推送沒有運作 (在應用程式中、在應用程式外，或兩者)。

### <a name="causes"></a>原因
* 多次推送失敗是表示，Azure Mobile Engagement 的觸達，另一項進階的功能的 Azure Mobile Engagement 未正確地整合或升級需要 hello SDK toofix 新的 OS 或裝置平台的已知的問題。
* 測試只在應用程式的推播和只出的應用程式推入 toodetermine 動作是否在應用程式或超出應用程式的問題。
* 從 hello UI 和 hello API 當做測試疑難排解的步驟 toosee 哪些其他錯誤資訊會使用這兩個位置。
* 應用程式外推播通知會無法運作，除非同時 Azure Mobile Engagement 觸達已經整合 hello SDK 中。
* 如果憑證無效，或正在正確使用 PROD 與DEV 正確 (僅限 iOS)。 (**附註：** "不在應用程式 「 推播通知無法傳遞 tooiOS，如果您有兩個 hello 開發 (DEV) 和實際執行環境 （生產環境） 您的應用程式上安裝的版本 hello 相同自 hello 安全性權杖相關聯的裝置使用您的憑證可能由 Apple 失效。 tooresolve 這個問題，請解除安裝 hello 開發和生產環境應用程式版本，然後重新安裝只有 hello 一個版本在您的裝置上。)
* 應用程式外推入計數的處理方式不同在不同的平台 （iOS 顯示較少資訊比 Android 原生推播通知已停用裝置 hello API 推入統計資料可以提供比 hello UI 的詳細資訊）。
* 應用程式外推送可以由客戶在作業系統層級 (iOS 與 Android) 封鎖。
* 應用程式外推播通知會顯示 hello Azure Mobile Engagement UI 中停用，如果不正確，整合，但可能從 hello API 會以無訊息模式失敗。
* 在應用程式除非同時 Azure Mobile Engagement 觸達已經整合 hello SDK 中，將無法運作推播通知。
* GCM 與 ADM 推播通知將無法運作，除非 Azure Mobile Engagement hello 特定伺服器已經整合在 hello SDK (僅 Android)。
* 在應用程式和應用程式應該是推播通知的測試個別 toodetermine 如果是發送或觸達的問題。
* 在應用程式推入需要該 hello 應用程式會收到開啟 toobe。
* 在應用程式推入通常會安裝 toobe 以選擇加入或退出應用程式資訊標記進行篩選。
* 如果您使用自訂分類在觸達 toodisplay 應用程式內通知、 需要 toofollow hello 正確生命週期的 hello 通知，否則可能不會清除 hello 通知時 hello 使用者關閉它。
* 如果您沒有結束日期開始活動，且裝置收到 hello 中應用程式通知，但不會顯示它尚未，hello 使用者仍會收到 hello 通知 hello 下次登入 hello 應用程式，即使您以手動方式結束 hello 行銷活動。
* 與 hello 推送 API 相關問題，請確認您真的想 toouse hello 推送 API 而不是 hello 觸達 API （因為 hello 觸達 API 的使用頻率），而且您不是令人混淆的 hello 「 裝載 」 和 「 通知 」 參數。
* 測試您的推播宣傳活動與透過 WIFI 和 3g tooeliminate hello 網路連線問題的可能來源連接這兩個裝置。

## <a name="push-testing"></a>推送測試
### <a name="issue"></a>問題
* 可傳送推播通知 tooa 特定裝置根據裝置識別碼。

### <a name="causes"></a>原因
* 測試裝置的安裝程式以不同的方式每個平台，但是測試裝置上的應用程式中引發的事件，並尋找您的裝置識別碼 hello 入口網站中應該運作 toofind 您用於所有平台的裝置識別碼。
* 測試裝置與 IDFA 與IDFV 搭配使用時運作方式不同 (僅 iOS)。

## <a name="push-customization"></a>自訂推送
### <a name="issue"></a>問題
* 進階推送內容項目無法運作 (徽章、響鈴、震動、圖片等)。
* 推播通知的連結沒有作用 （不在應用程式，在應用程式、 tooa 網站、 應用程式中的 tooa 位置）。
* 推入不是發送統計資料顯示 tooas 如預期般許多人 （太多或傳送不足）。
* 重複推送，並且收到兩次。
* 無法為 Azure Mobile Engagement 推送註冊測試裝置 (使用您自己的 Prod 或 DEV 應用程式)。

### <a name="causes"></a>原因
* toolink tooa 中特定位置的應用程式需要 「 類別 」 (僅 Android)。
* 深層連結配置後按一下推播通知的 tooredirect 使用者 tooan 替代位置需要 toobe 中所建立和管理您的應用程式和 hello 裝置作業系統不是由 Mobile Engagement 直接。 (**附註：**不在應用程式通知無法連結直接 tooin iOS 應用程式位置，它們可以 Android。)
* 外部影像伺服器需要 toobe 無法 toouse HTTP 「 GET 」 和 「 前端 」 的大圖片推播通知 toowork (僅 Android)。
* 在您的程式碼中，您可以 hello Azure Mobile Engagement 代理程式時開啟 hello 鍵盤時，停用，讓您的程式碼重新啟動之後 hello 鍵盤已關閉的 hello 鍵盤不會影響 hello 外觀 hello Azure Mobile Engagement 代理程式(僅限 iOS) 的通知。
* 部分項目在測試模擬中沒有作用，只有在實際活動 (徽章、響鈴、震動、圖片等) 中才會有作用。
* 當您使用 hello 按鈕時，會記錄資料的任何伺服器端太"test"推播不通知。 只會記錄實際推送活動的資料。
* toohelp 隔離您的問題，請使用進行疑難排解： 測試，模擬，與實際的活動，因為它們都各自的運作方式稍有不同。
* hello 的您在 「 」 中的應用程式 」 和 「 任何時間 」 活動會排定的 toorun 的時間長度可以影響傳遞數字因為活動只會傳遞 toousers 」 中之應用程式"hello 活動執行時 （而且其裝置設定的使用者設定 tooreceive通知 「 不足應用程式 」）。
* hello 差異如何 Android 和 iOS 應用程式通知的控制代碼很難 toodirectly 比較 hello Android 和 iOS 應用程式版本之間的推送統計資料。 Android 相較於 iOS，提供較多作業系統層級的通知資訊。 Android 原生通知收到、 按一下，或刪除在 hello 通知中心，但除非 hello 通知按下 iOS 不會報告這項資訊的詳細報表。 
* hello 主要原因 「 推入 」 的數字都不同比不同比 「 傳送 」 的數字的到達活動的 於應用程式 」 及 「 不足 」 的應用程式通知的計數方式不同。 「 中 」 的應用程式通知由 Mobile Engagement 處理，但是 「 不在應用程式 」 通知由您的裝置 hello OS 中的 hello 通知中心處理。

## <a name="push-targeting"></a>推送目標
### <a name="issue"></a>問題
* 內建目標未如預期般運作。
* 應用程式資訊標記目標未如預期般運作。
* 地理位置目標未如預期般運作。
* 語言選項未如預期般運作。

### <a name="causes"></a>原因
* 請確定您已上傳應用程式資訊標記透過 hello Azure Mobile Engagement UI 或應用程式開發介面。
* 節流 hello 推送速度或推播配額 hello 應用程式層級或在 hello 活動層級的限制 hello 觀眾可以防止個人接收特定推入，即使它們符合您目標的準則。 
* 設定「語言」和依據國家或地區設定目標不同，這也和依據地理位置、手機位置或 GPS 定位位置設定目標不同。
* hello"預設語言 」 中的 hello 訊息會傳送 tooany 客戶，且沒有設定 tooone hello 替代語言，您指定的裝置。

## <a name="push-scheduling"></a>推送排程
### <a name="issue"></a>問題
* 推送排程未如預期般運作 (過早或延遲傳送)。

### <a name="causes"></a>原因
* 時區可以排程的問題，尤其是使用 hello 畷樾簅時區。
* 進階推送功能可能會延遲推送。
* 因為 Azure Mobile Engagement 可能擁有 toorequest hello 電話即時資料，然後才傳送推播，目標為依據的電話 （而不是應用程式資訊標記） 的設定可能會延遲推播通知。
* 沒有結束日期的情況下建立的活動在 hello 裝置上本機儲存 hello 推入並將其顯示 hello 即使手動結束 hello 活動開啟 hello 應用程式的下一次。
* 啟動多個活動在 hello 相同的時間可能需要較長的時間 tooscan 您使用者的基底 （四個，最多一次嘗試 tooonly 開始一個活動，也目標 tooyour 作用中使用者，讓舊的使用者不需要掃描 toobe）。
* 如果您使用 hello"忽略受眾，推入將會傳送 hello 應用程式開發介面透過 toousers 」 選項 hello 「 活動 」 一節中的觸達活動，不會自動傳送 hello 行銷活動，您需要 toosend 它以手動方式透過 hello 觸達 API。
* 如果您使用自訂分類在觸達 toodisplay 應用程式內通知、 需要 toofollow hello 正確生命週期的通知，否則可能不會清除 hello 通知時 hello 使用者關閉它。

