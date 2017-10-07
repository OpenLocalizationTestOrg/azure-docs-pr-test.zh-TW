---
title: aaaTemplates
description: "本主題說明 Azure 通知中樞的範本。"
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: a41897bb-5b4b-48b2-bfd5-2e3c65edc37e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 0149f0c7473e5a4b952905bc8217582b58db2a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="templates"></a>範本
## <a name="overview"></a>概觀
範本可讓用戶端應用程式 toospecify hello 確切格式的 hello 通知它想 tooreceive。 使用範本，應用程式可以了解幾個不同的優點，包括下列 hello:

* 跨平台的後端
* 個人化的通知
* 用戶端版本獨立性
* 容易當地語系化

本節提供如何為您的裝置目標跨平台和 toopersonalize toouse 範本 toosend 無從驗證平台通知廣播通知 tooeach 裝置的兩個深入了解範例。

## <a name="using-templates-cross-platform"></a>跨平台使用範本
hello 標準方式 toosend 推播通知是 toosend，每個通知的傳送，toobe 特定裝載 tooplatform 通知服務 （WNS、 APNS）。 範例，toosend 警示的 tooAPNS hello 裝載為 Json 物件的下列形式的 hello:

    {"aps": {"alert" : "Hello!" }}

toosend 類似的快顯訊息上的 Windows 市集應用程式，hello XML 裝載如下所示：

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

您可以為 MPNS (Windows Phone) 和 GCM (Android) 平台建立類似的承載。

這項需求會強制 hello 應用程式後端 tooproduce 不同的裝載的每個平台，並有效地讓 hello 後端負責 hello 展示層的 hello 應用程式的一部分。 一些考量包括當地語系化和圖形配置 (尤其是針對包含各種類型之磚通知的「Windows 市集」應用程式)。

hello 通知中樞範本功能可讓用戶端應用程式 toocreate 特殊登錄，稱為另外包含 toohello 組標記，範本的範本註冊。 hello 通知中樞範本功能可讓用戶端應用程式 tooassociate 裝置範本是否正在使用的安裝 （慣用） 或註冊。 由於 hello 前面裝載範例 hello 平台無關的唯一資訊是，hello 實際警示訊息 (Hello ！)。 範本是一組的 hello 通知中樞上如何 tooformat 平台獨立訊息 hello 註冊該特定用戶端應用程式的指示。 在上述範例中的 hello，hello 平台獨立訊息是單一的屬性：**訊息 = Hello ！**。

下列圖片的 hello 說明上述程序的 hello:

![](./media/notification-hubs-templates/notification-hubs-hello.png)

hello iOS 用戶端應用程式註冊的 hello 範本如下所示：

    {"aps": {"alert": "$(message)"}}

hello 對應 hello Windows 市集用戶端應用程式範本是：

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

請注意，hello 實際的訊息是要替換 hello 運算式 $（訊息）。 這個運算式會指示 hello 通知中樞時傳送訊息 toothis 特定註冊，toobuild 遵循它和交換器 hello 共通的值中的訊息。

如果您正在使用安裝模型，hello 安裝 「 範本 」 金鑰會保留多個範本的 JSON。 如果您正在使用的註冊模型，hello 用戶端應用程式可以建立多個註冊順序 toouse 中多個範本。例如，警示訊息的範本和磚範本更新。 用戶端應用程式也可以混合使用原生註冊 (無範本的註冊) 與範本註冊。

hello 通知中樞傳送一則通知之每個範本，而不考慮 toohello 所屬相同的用戶端應用程式。 此行為可使用的 tootranslate 平台獨立通知到多個通知。 例如，hello 通知中樞可以順暢地轉譯在快顯通知和磚更新，而不需要知道它的 hello 後端 toobe 相同平台獨立訊息 toohello。 請注意，某些平台 (例如，iOS) 可能會摺疊多個通知 toohello 相同的裝置，如果在短時間內進行傳送。

## <a name="using-templates-for-personalization"></a>使用範本來進行個人化
另一個優點 toousing 範本是 hello 能力 toouse 通知中樞 tooperform 註冊每個個人化的通知。 例如，請考慮天氣應用程式，以顯示磚與 hello 天氣的特定位置。 使用者可以在攝氏或華氏溫度及單日或五日預測之間做選擇。 使用範本，每個用戶端應用程式安裝可以註冊所需的 hello 格式 (1 天攝氏、 1 天華氏，5 天攝氏，5 天華氏)，而且有傳送單一訊息，其中包含所有 hello 資訊所需 toofill 那些 hello 後端範本 （例如，五天預測與攝氏和華氏度為單位）。

hello 範本 hello 一天預測與攝氏溫度如下所示：

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

hello 訊息傳送 toohello 通知中樞會包含下列屬性的所有 hello:

<table border="1">

<tr><td>day1_image</td><td>day2_image</td><td>day3_image</td><td>day4_image</td><td>day5_image</td></tr>

<tr><td>day1_tempC</td><td>day2_tempC</td><td>day3_tempC</td><td>day4_tempC</td><td>day5_tempC</td></tr>

<tr><td>day1_tempF</td><td>day2_tempF</td><td>day3_tempF</td><td>day4_tempF</td><td>day5_tempF</td></tr>
</table><br/>

藉由使用此模式，hello 後端只傳送單一訊息而不需要 toostore hello 應用程式使用者的特定個人化選項。 下列圖片的 hello 說明這種情況：

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-tooregister-templates"></a>如何 tooregister 範本
tooregister 範本使用 hello 安裝模型 （慣用） 或 hello 註冊模型，請參閱[註冊管理](notification-hubs-push-notification-registration-management.md)。

## <a name="template-expression-language"></a>範本運算式語言
範本是有限的 tooXML 或 JSON 文件格式。 此外，您只能將運算式放在特定的位置；例如，如果是 XML，只能放在節點屬性或值中，如果是 JSON，則只能放在字串屬性值中。

hello 下表顯示允許範本中的 hello 語言：

| 運算是 | 說明 |
| --- | --- |
| $(prop) |參考 tooan hello 給定名稱的事件屬性。 屬性名稱不區分大小寫。 如果沒有 hello 屬性，這個運算式會解析至 hello 屬性的文字值或空字串。 |
| $(prop, n) |如以上所述，但 hello 文字已明確地裁剪成 n 個字元，例如 $（標題，20） 裁剪的 hello title 屬性的 hello 內容在 20 個字元。 |
| .(prop, n) |為更新版本，但 hello 文字的後置字元三個點時，它會裁剪。 hello hello 的大小總計裁剪字串，而且 hello 後置詞不會超過 n 個字元。 .（標題，20）"This is hello 標題列 」 結果中的輸入屬性與**hello 標題...** |
| %(prop) |除了該 hello 輸出類似 too$(name) 是 URI 編碼。 |
| #(prop) |用於 JSON 範本 (例如，用於 iOS 與 Android 範本)。<br><br>此函式運作方式完全 hello 相同為 $(prop) 先前指定 JSON 範本 （例如，Apple 範本） 中使用時除外。 在此情況下，如果此函式不會圍繞著"{'，'}"(，例如 'myJsonProperty': '# （名稱）')，它會評估 Javascript 格式，例如 regexp tooa 數字和: (0 &#124; (&#91; 1-9 &#93; &#91; 0-9 &#93;*))(\.&#91; 0-9 &#93; +)？((&#124;E) (+ &#124;-) 嗎？ （& s) #91; 0-9 &#93; +)？，hello 輸出 JSON 是數字，然後。<br><br>例如，‘badge : ‘#(name)’ 會變成 ‘badge’ : 40 (而不是 ‘40‘)。 |
| ‘text’ 或 “text” |常值。 常值包含以單引號或雙引號括住的任意文字。 |
| expr1 + expr2 |hello 串連運算子結合成單一字串的兩個運算式。 |

hello 運算式可以是任何 hello 前面表單。

當使用串連，必須與 {} 括住 hello 整個運算式。 例如 {$(prop) + ‘ - ’ + $(prop2)}。 |

例如，hello 以下不是有效的 XML 範本：

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


如上面所述，使用串連時，運算式必須包含在大括號中。 例如：

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

