---
title: "Mobile Engagement Web SDK Api aaaAzure |Microsoft 文件"
description: "Azure Mobile Engagement hello 最新更新和 hello Web SDK 的程序"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8a87d5ac-d8b7-4a0d-bdee-414dbcc561b2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: ec1261d6ad573b8c3ad6d5f616ab7bbe560d6fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-mobile-engagement-api-in-a-web-application"></a>使用 web 應用程式中的 hello Azure Mobile Engagement 應用程式開發介面
這份文件是加法 toohello 文件，告訴您如何太[web 應用程式中整合 Mobile Engagement](mobile-engagement-web-integrate-engagement.md)。 它提供有關如何 toouse hello tooreport Azure Mobile Engagement 應用程式開發介面的詳細資料您的應用程式統計資料。

hello Mobile Engagement 應用程式開發介面由提供 hello`engagement.agent`物件。 hello Azure Mobile Engagement Web SDK 別名是的預設`engagement`。 您可以重新定義從 hello SDK 設定此別名。

## <a name="mobile-engagement-concepts"></a>Mobile Engagement 概念
hello 下列部分精簡常見[Mobile Engagement 概念](mobile-engagement-concepts.md)hello web 平台。

### <a name="session-and-activity"></a>`Session`和`Activity`
如果兩個活動之間的多個數秒鐘，hello 使用者停留閒置，hello 使用者的活動順序分成兩個不同的工作階段。 這些幾秒鐘的時間稱為 hello 工作階段逾時。

如果 web 應用程式不會宣告 hello 結束使用者活動本身 (透過呼叫 hello`engagement.agent.endActivity`函式)，hello Mobile Engagement 伺服器自動到期 hello hello 應用程式頁面上關閉後的 3 分鐘內的使用者工作階段。 這稱為 hello 伺服器工作階段逾時。

### `Crash`
根據預設，不會建立無法攔截的 JavaScript 例外狀況的自動報告。 不過，您也可以回報當機的 hello`sendCrash`函式 （請參閱報告損毀的 hello > 一節）。

## <a name="reporting-activities"></a>報告活動
使用者活動上的報告包括當使用者啟動新的活動與 hello 使用者結束 hello 目前活動時。

### <a name="user-starts-a-new-activity"></a>使用者啟動新的活動
    engagement.agent.startActivity("MyUserActivity");

您需要 toocall`startActivity()`變更每個階段的使用者活動。 hello 第一個呼叫 toothis 函式會啟動新的使用者工作階段。

### <a name="user-ends-hello-current-activity"></a>使用者結束 hello 目前活動
    engagement.agent.endActivity();

您需要 toocall`endActivity()`至少一次當 hello 使用者完成其最後一個活動。 這會通知 hello Mobile Engagement Web SDK hello 使用者目前閒置，並 hello 使用者工作階段需要 toobe hello 工作階段逾時過期之後關閉。 如果您呼叫`startActivity()`hello 工作階段逾時到期前，只要繼續進行 hello 工作階段。

因為沒有可靠的 hello 導覽器] 視窗已關閉時呼叫，通常很難或是無法 toocatch hello 結尾 web 環境內的使用者活動。 原因是 hello 伺服器自動到期的 Mobile Engagement hello hello 應用程式頁面上關閉後的 3 分鐘內的使用者工作階段。

## <a name="reporting-events"></a>報告事件
報告事件涵蓋了工作階段事件和獨立事件。

### <a name="session-events"></a>工作階段事件
工作階段事件通常是使用者執行的 hello 使用者工作階段期間使用的 tooreport hello 動作。

**不含額外資料的範例：**

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

**含額外資料的範例：**

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a>獨立事件
不同於工作階段事件獨立發生的事件工作階段的 hello 內容之外。

針對那種情況，請使用 ``engagement.agent.sendEvent``，而不是 ``engagement.agent.sendSessionEvent``。

## <a name="reporting-errors"></a>報告錯誤
報告錯誤涵蓋了工作階段錯誤和獨立錯誤。

### <a name="session-errors"></a>工作階段錯誤
工作階段錯誤通常是影響的 hello 使用者 hello 使用者工作階段期間的使用的 tooreport hello 錯誤。

**不含額外資料的範例：**

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

**含額外資料的範例：**

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a>獨立錯誤
不同於工作階段錯誤，可能會發生工作階段的 hello 內容以外的獨立錯誤。

針對那種情況，請使用 `engagement.agent.sendError`，而不是 `engagement.agent.sendSessionError`。

## <a name="reporting-jobs"></a>報告工作
報告作業涵蓋報告在作業期間發生的錯誤和事件，以及報告當機。

**範例：**

如果您想 toomonitor AJAX 要求時，您可以使用下列 hello:

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
      // [...]
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-errors-during-a-job"></a>報告於作業期間發生的錯誤
錯誤可能是相關的 tooa 執行而不是 toohello 目前使用者工作階段的作業。

**範例：**

如果您想要 tooreport 錯誤如果 AJAX 要求，失敗：

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
        // [...]
        if (xhr.status == 0 || xhr.status >= 400) {
          engagement.agent.sendJobError('publish_xhr', 'publish', {status: xhr.status, statusText: xhr.statusText});
        }
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-events-during-a-job"></a>在作業期間報告事件
事件可能會執行作業，而不是目前使用者工作階段 toohello，這 toohello 相關的 tooa`engagement.agent.sendJobEvent`函式。

此函式的運作方式與 `engagement.agent.sendJobError`完全相同。

### <a name="reporting-crashes"></a>報告當機
使用 hello`sendCrash`函式 tooreport 手動損毀。

hello`crashid`引數是可識別 hello 損毀類型的字串。
hello`crash`引數通常是做為字串 hello 損毀 hello 堆疊追蹤。

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a>額外的參數
您可以附加任意資料 tooan 事件、 錯誤、 活動或工作。

hello 資料可以是任何的 JSON 物件 （但不是陣列或基本類型）。

**範例：**

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a>限制
套用 tooextra 參數的限制是在規則運算式的索引鍵、 值類型和大小的 hello 部分。

#### <a name="keys"></a>之間的信任
Hello 物件中的每個索引鍵必須符合下列規則運算式的 hello:

    ^[a-zA-Z][a-zA-Z_0-9]*

這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。

#### <a name="values"></a>值
值為有限的 toostring、 數字和 Boolean 類型。

#### <a name="size"></a>大小
額外項目是限制的 too1，024 每個呼叫 （在 hello Mobile Engagement Web SDK 會將其編碼 JSON 中） 之後的字元。

## <a name="reporting-application-information"></a>報告應用程式資訊
您可以手動追蹤資訊 （或任何其他應用程式特定資訊） 使用報告 hello`sendAppInfo()`函式。

請注意，這項資訊可以累加方式傳送。 只有 hello 最新值的特定索引鍵會保留特定裝置。

類似事件的額外功能，您可以使用任何 JSON 物件 tooabstract 應用程式資訊。 請注意，陣列或子物件會視為一般字串 (使用 JSON 序列化)。

**範例：**

以下是針對傳送嗨使用者的性別和生日的程式碼範例：

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a>限制
Tooapplication 資訊適用於的限制是 hello 區域的金鑰和大小的規則運算式中。

#### <a name="keys"></a>之間的信任
Hello 物件中的每個索引鍵必須符合下列規則運算式的 hello:

    ^[a-zA-Z][a-zA-Z_0-9]*

這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。

#### <a name="size"></a>大小
應用程式的資訊是有限的 too1，024 每個呼叫 （在 hello Mobile Engagement Web SDK 會將其編碼 JSON 中） 之後的字元。

在上述範例中的 hello，hello JSON 傳送 toohello 伺服器是 44 個字元：

    {"birthdate":"1983-12-07","gender":"female"}
