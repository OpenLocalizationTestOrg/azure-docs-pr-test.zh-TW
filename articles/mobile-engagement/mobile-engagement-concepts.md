---
title: "aaaMobile Engagement 概念 |Microsoft 文件"
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
ms.openlocfilehash: 5aa7f28c00cd641a36a6e040c6b13d802ea6ae41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-concepts"></a>Azure Mobile Engagement 概念
Mobile Engagement 會定義幾個概念常見 tooall 支援平台。 本文會簡短說明這些概念。

如果您是新 tooMobile Engagement 這篇文章會是不錯的起點。 也請確定 tooread hello 文件特定 toohello 平台使用，因為它會精簡 hello 概念更多詳細資料和範例，以及可能限制此文件中所述。

## <a name="devices-and-users"></a>裝置和使用者
Mobile Engagement 藉由為每台裝置產生唯一識別碼來識別使用者。 這個識別項稱為 hello 裝置識別碼 (或`deviceid`)。 產生的所有應用程式執行 hello 相同的方式共用裝置 hello 相同裝置識別碼。

隱含的這表示，Mobile Engagement 會考慮一個裝置 toobelong tooexactly 一個使用者，因此，使用者與裝置都相當的概念。

## <a name="sessions-and-activities"></a>工作階段和活動
工作階段是使用 hello hello 時間 hello 使用者的使用者，所執行的應用程式一開始使用它，直到 hello 使用者停止。

活動是給定的子 hello 一位使用者所執行的應用程式一部分的一個用法 （通常是畫面上，但它可以是任何項目適合 toohello 應用程式）。

使用者一次只能執行一個活動。

活動由 （有限的 too64 字元） 的名稱，並可以選擇性地嵌入某些額外的資料 （hello 限制為 1024 個位元組）。

自動計算工作階段的使用者所執行的活動 hello 序列中的資料。 工作階段開始時 hello 使用者開始其第一個活動，他完成他的最後一個活動時，就會停止。 這表示工作階段不需要 toobe 明確啟動或停止。 相反地，活動會明確地開始或停止。 如果沒有報告任何活動，則不會報告任何工作階段。

## <a name="events"></a>事件
事件是使用的 tooreport 立即動作 （例如按鈕按下或由使用者所讀取的文件）。

事件可能是相關的 toohello 目前工作階段，tooa 執行作業，或獨立事件。

事件由 （有限的 too64 字元） 的名稱，並可以選擇性地嵌入某些額外的資料 （hello 限制為 1024 個位元組）。

## <a name="error"></a>錯誤
錯誤是使用的 tooreport 問題正確地偵測到的 hello 應用程式 （例如不正確的使用者動作或應用程式開發介面呼叫失敗）。

錯誤可能是相關的 toohello 目前工作階段，tooa 執行作業，或它可以是一個獨立的錯誤。

錯誤由 （有限的 too64 字元） 的名稱，並可以選擇性地嵌入某些額外的資料 （hello 限制為 1024 個位元組）。

## <a name="job"></a>作業
作業會使用的 tooreport 動作具有持續時間 （持續時間的 API 呼叫，例如顯示的廣告時間、 持續時間的背景工作或使用者動作的持續時間）。

作業不是相關的 tooa 工作階段，因為沒有任何使用者互動的 hello 背景來執行工作。

作業由 （有限的 too64 字元） 的名稱，且可以選擇性地嵌入某些額外的資料 （hello 限制為 1024 個位元組）。

## <a name="crash"></a>當機
由 hello Mobile Engagement SDK tooreport 應用程式損毀的失敗而無法偵測的 hello 應用程式的問題進行它自動發出損毀。

## <a name="application-information"></a>應用程式資訊
應用程式資訊 （或應用程式資訊） 是使用的 tootag 使用者，也就是 tooassociate （不同之處在於應用程式資訊會儲存在 hello hello Azure Mobile Engagement 平台上的伺服器端上，這是類似的 tooweb cookie） 應用程式的某些資料 toohello 使用者。

使用 hello Mobile Engagement SDK 的 API，或使用 hello Mobile Engagement 平台裝置 API，您可以註冊應用程式資訊。

應用程式資訊是索引鍵/值組相關聯的 tooa 裝置。 hello 索引鍵是 hello 名稱 hello 應用程式資訊 （有限的 too64 ASCII 字母 [的 A-ZA-Z]，[0-9] 數字和底線 [__]）。 hello 值 （有限的 too1024 字元） 可以是任何字串、 整數、 日期 (yyyy-MM-dd) 或布林值 （true 或 false）。

任何數目的應用程式資訊可以是相關聯的 tooa 裝置，hello hello Mobile Engagement 定價條件所定義的限制範圍內。 一個指定的索引鍵，Mobile Engagement 只會追蹤的最新值集 hello （沒有記錄）。 設定或變更的應用程式資訊的 hello 值強制 Mobile Engagement toore-評估此應用程式上設定的受眾準則資訊 （如果有的話） 表示該應用程式資訊為使用的 tootrigger 即時推播通知。

## <a name="extra-data"></a>額外的資料
額外的資料 （或額外項目） 會任意資料可以附加的 tooevents、 錯誤、 活動與工作。

結構化的額外項目同樣 tooJSON 物件： 這些語言的索引鍵/值組的樹狀結構。 索引鍵是有限的 too64 ASCII 字母 [的 A-ZA-Z]、 [0-9] 數字和底線 [__]） 和 hello 的額外項目大小總計為有限的 too1024 （一次編碼字元在 JSON 中的 hello Mobile Engagement SDK）。

hello 的索引鍵/值組的整個樹狀結構會儲存為 JSON 物件。 不過，只有 hello 第一個層級索引鍵/值，會分解的 toobe 直接存取 toosome 進階函式，例如區段 （例如，您可以輕鬆地定義區段稱為 「 SciFi 風扇 」 所做的所有使用者有傳送至少 10 次 hello 事件名為"content_viewed"hello 額外金鑰 「 有效 」 組 toohello 值"scifi"hello 在上個月）。 因此強烈建議使用純量值 （例如，字串、 日期、 整數或布林值） 的索引鍵/值組的簡單清單所組成 toosend 唯一額外項目。

## <a name="next-steps"></a>後續步驟
* [適用於 Azure Mobile Engagement 的 Windows 通用 SDK 概觀](mobile-engagement-windows-store-sdk-overview.md)
* [適用於 Azure Mobile Engagement 的 Windows Phone Silverlight SDK 概觀](mobile-engagement-windows-phone-sdk-overview.md)
* [Azure Mobile Engagement iOS SDK](mobile-engagement-ios-sdk-overview.md)
* [適用於 Azure Mobile Engagement 的 Android SDK](mobile-engagement-android-sdk-overview.md)

