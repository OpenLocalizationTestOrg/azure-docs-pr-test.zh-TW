---
title: "Mobile Engagement 概念 | Microsoft Docs"
description: "Azure Mobile Engagement 概念"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8d19abd1-0a6c-4772-9fa5-5e99980ac5da
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 8450651528007b4527366b89a6ad7615169f93c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement-concepts"></a>Azure Mobile Engagement 概念
Mobile Engagement 定義所有支援平台共同的一些概念。 本文會簡短說明這些概念。

如果您不熟悉 Mobile Engagement，本文會是一個不錯的起點。 也請務必閱讀您所使用平台的專屬文件，因為它會精簡本文中所述概念的更多詳細資料和範例，以及可能的限制。

## <a name="devices-and-users"></a>裝置和使用者
Mobile Engagement 藉由為每台裝置產生唯一識別碼來識別使用者。 這個識別碼稱為裝置識別碼 (或 `deviceid`)。 它產生的方式會讓相同裝置的所有執行中應用程式共用相同的裝置識別碼。

這隱含地表示，Mobile Engagement 會將一台裝置視為只屬於一位使用者，因此，使用者和裝置是對等概念。

## <a name="sessions-and-activities"></a>工作階段和活動
工作階段是由使用者執行的一次應用程式使用，從使用者開始使用的時間，直到使用者停止的時間為止。

活動是一位使用者所執行的應用程式特定子部分的一次使用 (通常是一個畫面，但可以是任何適合該應用程式的東西)。

使用者一次只能執行一個活動。

活動是以名稱來識別 (限制為 64 個字元)，而且可以選擇性地嵌入一些額外的資料 (在 1024 個位元組的限制內)。

工作階段會自動從使用者執行的活動序列運算。 工作階段會在使用者開始他的第一個活動時開始，在他完成他的最後一個活動時停止。 這表示工作階段不需要明確地開始或停止。 相反地，活動會明確地開始或停止。 如果沒有報告任何活動，則不會報告任何工作階段。

## <a name="events"></a>事件
事件用來報告立即動作 (像是按下按鈕或是使用者閱讀了文章)。

事件可以與目前工作階段或執行中的工作相關，也可以是獨立存在的事件。

事件是以名稱來識別 (限制為 64 個字元)，而且可以選擇性地嵌入一些額外的資料 (在 1024 個位元組的限制內)。

## <a name="error"></a>錯誤
錯誤用來報告應用程式正確偵測到的問題 (例如不正確的使用者動作，或 API 呼叫失敗)。

錯誤可以與目前工作階段或執行中的工作相關，也可以是獨立存在的錯誤。

錯誤是以名稱來識別 (限制為 64 個字元)，而且可以選擇性地嵌入一些額外的資料 (在 1024 個位元組的限制內)。

## <a name="job"></a>工作 (Job)
工作用來報告具有持續時間的動作 (像是 API 呼叫持續時間、廣告的顯示時間、背景工作的持續時間，或使用者動作的持續時間)。

工作與工作階段無關，因為可以在背景執行工作，而沒有任何使用者互動。

工作是以名稱來識別 (限制為 64 個字元)，而且可以選擇性地嵌入一些額外的資料 (在 1024 個位元組的限制內)。

## <a name="crash"></a>當機
當機是由 Mobile Engagement SDK 自動發出以報告應用程式失敗，其中是由應用程式未偵測到的問題使它當機的。

## <a name="application-information"></a>應用程式資訊
應用程式資訊 (或應用程式資訊 (app info)) 可用來標記使用者，也就是將一些資料與應用程式的使用者建立關聯 (這點類似於 Web Cookie，不過應用程式資訊會儲存在 Azure Mobile Engagement 平台上的伺服器端)。

應用程式資訊可以使用 Mobile Engagement SDK API 或使用 Mobile Engagement 平台裝置 API 來登記。

應用程式資訊是與裝置相關聯的索引鍵/值組。 索引鍵是應用程式資訊的名稱 (限制為 64 個 ASCII 字元 [zA-A-Z]、數字 [0-9] 和底線 [__])。 值 (限制為 1024 個字元) 可以是任何字串、整數、日期 (-yyyy-mm-dd) 或布林值 (true 或 false)。

任何數目的應用程式資訊可以與裝置相關聯，只要在 Mobile Engagement 定價條件所定義的限制內即可。 針對一個指定的索引鍵，Mobile Engagement 只會追蹤最新設定的值 (沒有記錄)。 設定或變更應用程式資訊的值會強制 Mobile Engagement 重新評估此應用程式資訊上設定的對象準則 (如果有的話)，這表示應用程式資訊可以用來觸發即時推送。

## <a name="extra-data"></a>額外的資料
額外的資料 (或額外項目) 是一些可以附加到事件、錯誤、活動和工作的任意資料。

額外項目的結構與 JSON 物件類似：包含索引鍵/值組的樹狀結構。 索引鍵限制為 64 個 ASCII 字母 [a A-ZA-Z]、數字 [0-9] 和底線 [__])，而額外項目的總大小則限制為 1024 個字元 (由 Mobile Engagement SDK 以 JSON 編碼之後)。

索引鍵/值組的整個樹狀結構會儲存為 JSON 物件。 不過，只有索引鍵/值的第一個層級會分解以便可供一些進階的函式直接存取，例如 Segments (例如，您可以輕鬆地定義稱為 "SciFi fans" 的區段，它是由上個月傳送至少 10 次事件名為 "content_viewed" 事件的所有使用者所構成，且額外的索引鍵 "content_type" 設定為 "scifi" 值)。 因此強烈建議只傳送使用純量值 (例如字串、日期、整數或布林值) 的索引鍵/值組簡單清單所組成的額外項目。

## <a name="next-steps"></a>後續步驟
* [適用於 Azure Mobile Engagement 的 Windows 通用 SDK 概觀](mobile-engagement-windows-store-sdk-overview.md)
* [適用於 Azure Mobile Engagement 的 Windows Phone Silverlight SDK 概觀](mobile-engagement-windows-phone-sdk-overview.md)
* [Azure Mobile Engagement iOS SDK](mobile-engagement-ios-sdk-overview.md)
* [適用於 Azure Mobile Engagement 的 Android SDK](mobile-engagement-android-sdk-overview.md)

