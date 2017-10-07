---
title: "Azure Active Directory B2C︰使用語言自訂 | Microsoft Docs"
description: 
services: active-directory-b2c
documentationcenter: 
author: sama
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: sama
ms.openlocfilehash: a8e4037014f5adf929dac7b5dc4db72ba0f5b292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-using-language-customization"></a>Azure Active Directory B2C︰使用語言自訂

>[!NOTE] 
>這項功能處於公開預覽狀態。  建議您在使用這項功能時，使用測試租用戶。  我們不打算 hello 預覽 toohello 公開上市版本中，從任何重大變更，但保留 hello 右 toomake 這類變更 tooimprove hello 功能。  一旦您已經有機會 tootry 功能，請提供您的體驗的意見反應及如何使其更好。  您可以透過提供意見反應 hello Azure 入口網站使用上 hello 右上方的 hello 的臉正面工具。   如果有一項業務需求為您 toogo 即時 hello 預覽階段期間使用這項功能，讓我們知道您的案例，我們可以提供您的 hello 適當指引及取得協助。  您可以透過 [aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com) 來與我們連絡。

語言自訂，可讓您 toochange 使用者走 tooa 不同語言 toosuit 您客戶的需求。  我們提供 36 種語言的翻譯 (請參閱[其他資訊](#additional-information))。  即使茪擩槧槶只會提供您的體驗，您可以自訂 hello 頁面 toosuit 上的文字在您的需求。  

## <a name="how-does-language-customization-work"></a>語言自訂的運作方式為何？
語言自訂，可讓您 tooselect 使用者旅程是中可用哪些語言。  一旦啟用 hello 功能時，您可以提供 hello 查詢字串參數，ui_locales，從您的應用程式。  當您呼叫 Azure AD B2C 時，我們會轉譯頁面 toohello 地區設定，您已表示。  使用的組態類型可讓您在使用者旅程中的 hello 語言的完整控制權，並忽略 hello hello 客戶的瀏覽器的語言設定。 或者，您也可能不需要對客戶會看見哪種語言擁有這種程度的控制力。  如果您沒有提供 ui_locales 參數，其瀏覽器的設定取決於 hello 客戶經驗。  您仍然可以控制哪些使用者旅途的語言轉譯 tooby 將它新增為支援的語言。  如果客戶的瀏覽器設定 tooshow 語言不想 toosupport，然後選取支援的文化特性中的預設值改為所顯示的 hello 語言。

1. **ui 地區設定所指定語言**-使用者旅程一旦您啟用自訂語言，是此處指定的已翻譯的 toohello 語言
2. **瀏覽器要求語言**-如果已指定沒有 ui 地區設定，它會將轉譯 toohello 瀏覽器要求的語言，**如果它已包含在支援的語言**
3. **原則預設語言**-如果 hello 瀏覽器不會指定一種語言，或它不支援的其中一個指定，它會將轉譯 toohello 原則預設語言

>[!NOTE]
>如果您使用自訂的使用者屬性，您需要 tooprovide 您自己的翻譯。 如需詳細資訊，請參閱[自訂您的字串](#customize-your-strings)。
>

## <a name="support-uilocales-requested-languages"></a>支援 ui_locales 所要求的語言 
藉由啟用 '語言自訂' 的原則，您現在可以藉由加入 hello ui_locales 參數控制 hello 使用者旅程 hello 的語言。
1. [您可以依照這些步驟 toonavigate toohello B2C 功能刀鋒視窗上 hello Azure 入口網站。](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-app-registration#navigate-to-b2c-settings)
2. 瀏覽翻譯需 tooenable tooa 原則。
3. 按一下 [語言自訂]。
4. 讀取 hello 仔細警告。  啟用之後，您就無法關閉「語言自訂」。
5. 開啟 hello 功能，然後按一下**確定**。
6. 儲存您的原則上 hello 的左上角您**編輯原則**刀鋒視窗。

## <a name="select-which-languages-your-user-journey-supports"></a>選取您的使用者旅程所支援的語言 
建立允許您未提供 hello ui_locales 參數時，在轉譯的使用者之旅 toobe 語言的清單。
1. 透過前面的指示來確定您的原則已啟用「語言自訂」。
2. 從 [編輯原則] 刀鋒視窗中，選取 [語言自訂]。
3. 即會進入 tooyour**支援的語言**刀鋒視窗。  您可以從這裡選取 [新增語言]。
4. 選取所有您想要支援 toobe hello 語言。  

>[!NOTE]
>如果未提供 ui_locales 參數，然後 hello 頁面才翻譯的 toohello 客戶的瀏覽器語言其位於這份清單
>

5. 按一下**確定**hello 底部
6. 關閉 hello**語言自訂**刀鋒視窗和**儲存**您的原則。

## <a name="customize-your-strings"></a>自訂您的字串
'語言自訂' 可讓您 toocustomize 使用者旅程中的任何字串。
1. 請確定您的原則有語言自訂 hello 前述的指示從啟用。
2. 從 [編輯原則] 刀鋒視窗中，選取 [語言自訂]。
3. 從 hello 左側導覽功能表上，選取**下載內容**。
4. 選取您想要 tooedit hello 頁面。
5. 在 hello 下拉式清單中，選取您想要針對 tooedit hello 語言。
6. 按一下 [下載] 。 

這些步驟可讓您在 JSON 檔案，您可以使用 toostart 編輯您的字串。

### <a name="changing-any-string-on-hello-page"></a>變更在 hello 頁面上的任何字串
1. 從 JSON 編輯器的前述指示，下載開啟 hello JSON 檔案。
2. 尋找您想要 toochange 的 hello 項目。  您可以找到 hello `StringId` hello 字串，您要尋找或尋找 hello 的`Value`想 toochange。
3. 更新 hello`Value`具有您要顯示屬性。
4. 儲存 hello 檔案，並上傳您的變更。

### <a name="changing-extension-attributes"></a>變更擴充屬性
若您要尋找 toochange hello 字串的自訂使用者屬性，或想 tooadd 一個 toohello JSON 時，則為下列格式的 hello:
```JSON
{
  "LocalizedStrings": [
    {
      "ElementType": "ClaimType",
      "ElementId": "extension_<ExtensionAttribute>",
      "StringId": "DisplayName",
      "Override": false,
      "Value": "<ExtensionAttributeValue>"
    }
    [...]
}
```
>[!IMPORTANT]
>如果您需要 toooverride 字串時，請確定 tooset hello`Override`值太`true`。  如果 hello 值不會變更，則會忽略 hello 項目。 
>

取代`<ExtensionAttribute>`hello 的自訂使用者屬性的名稱。  
取代`<ExtensionAttributeValue>`與 hello 顯示新字串 toobe。

### <a name="using-localizedcollections"></a>使用 LocalizedCollections
如果您想要回應 tooprovide 值組清單，您需要 toocreate `LocalizedCollections`。  `LocalizedCollections` 是 `Name` 和 `Value` 的配對陣列。  hello`Name`是會顯示 hello`Value`是 hello 宣告中傳回的內容。  tooadd `LocalizedCollections`，它有下列格式的 hello:

```JSON
{
  "LocalizedStrings": [...],
  "LocalizedCollections": [{
      "ElementType":"ClaimType", 
      "ElementId":"<UserAttribute>",
      "TargetCollection":"Restriction",
      "Override": false,
      "Items":[
           {
                "Name":"<Response1>",
                "Value":"<Value1>"
           },
           {
                "Name":"<Response2>",
                "Value":"<Value2>"
           }
     ]
  }]
}
```
>[!IMPORTANT]
>如果您需要 toooverride 字串時，請確定 tooset hello`Override`值太`true`。  如果 hello 值不會變更，則會忽略 hello 項目。 
>

* `ElementId`是 hello 使用者屬性這`LocalizedCollections`會回應至
* `Name`hello 值顯示的 toohello 使用者
* `Value`已選取此選項時傳回 hello 宣告中

### <a name="upload-your-changes"></a>上傳您的變更
1. 當您完成 hello 變更 tooyour JSON 檔案時，瀏覽後 tooyour B2C 租用戶。
2. 從 [編輯原則] 刀鋒視窗中，選取 [語言自訂]。
3. 從 hello 左側導覽功能表上，選取**內容上傳**。
4. 選取您想做的變更 tooupload hello 頁面。
5. 如果您想 tooupload 您先前提供的 JSON 的語言，您會需要 toodelete hello 前一個項目。  您可以將它刪除即可 hello`...`在 hello 該語言的右邊，然後選取**刪除**。
6. 按一下**新增**hello 左上方。
7. 選取在 JSON 檔案 hello 語言。
8. 按一下 上 hello 右 hello 資料夾 按鈕，瀏覽您的 JSON 檔案。
9. 按一下 hello**上傳**上 hello hello 刀鋒視窗底部的按鈕。
10. 返回 tooyour**編輯原則**刀鋒視窗，然後按一下**儲存**。

## <a name="additional-information"></a>其他資訊
### <a name="recommendations-for-language-customization"></a>「語言自訂」的建議
我們建議僅將放在字串的項目 tooyour 語言資源您明確地想 tooreplace。  我們會強制執行編譯 JSON 翻譯超出大小限制 toohello 檔案。  如果您的檔案太大，它會影響使用者旅程 hello 的效能。
### <a name="page-ui-customization-labels-are-removed-once-language-customization-is-enabled"></a>「語言自訂」啟用後，系統就會移除頁面 UI 自訂標籤
當您啟用「語言自訂」時，系統會移除您先前使用頁面 UI 自訂對標籤所進行的編輯，但自訂使用者屬性除外。  這項變更是 tooavoid 衝突，您可以在其中編輯您的字串。  您可以繼續 toochange 標籤和其他字串上傳 '語言自訂' 中的語言資源。
### <a name="microsoft-is-committed-tooprovide-hello-most-up-to-date-translations-for-your-use"></a>Microsoft 於貴用戶使用的認可的 tooprovide hello 最新翻譯
我們會持續改善翻譯，並讓它們符合您的需求。  我們會找出錯誤和全域詞彙中的變更，使用者旅程中順暢地進行運作的 hello 更新。
### <a name="support-for-right-to-left-languages"></a>支援從右至左的語言
不支援由右至左的語言，如果您需要此功能，請在 [Azure 意見反應](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/19393000-provide-language-support-for-right-to-left-languag)投票給這項功能。
### <a name="social-identity-provider-translations"></a>社交識別提供者的翻譯
我們提供 hello ui_locales OIDC 參數 toosocial 登入，但有些社交身分識別提供者，包括 Facebook 和 Google 程式並不接受。 
### <a name="browser-behavior"></a>瀏覽器行為
Chrome 和 Firefox 同時要求其設定的語言，而且如果是支援的語言，它會顯示 hello 預設之前。  邊緣目前沒有要求的語言，且會直接 toohello 預設語言。
### <a name="known-issues"></a>已知問題
* 目前無法使用上傳設定檔編輯的原則中的 hello MFA 頁面的語言資源。
* `LocalizedCollections`不是值會產生 hello 回應類型視需要
### <a name="what-if-i-want-a-language-that-isnt-supported"></a>如果我想使用的語言不受支援會如何？
我們計劃 tooprovide 的這項功能，可讓您 tooupload 朝向 '自訂語言' JSON 資源擴充功能。  hello 功能可讓您 toospecify hello 名稱以及語言的任何語言程式碼，並提供*所有*hello 該語言的翻譯。  如果您需要這項功能，請將您的情況傳送給我們：[aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com)。  

### <a name="what-languages-are-supported"></a>支援哪些語言？

| 語言              | 語言代碼 |
|-----------------------|---------------|
| 孟加拉文                | bn            |
| 捷克文                 | cs            |
| 丹麥文                | da            |
| 德文                | de            |
| 希臘文                 | el            |
| English               | en            |
| 西班牙文               | es            |
| 芬蘭文               | fi            |
| 法文                | fr            |
| 古吉拉特文              | gu            |
| 北印度文                 | hi            |
| 克羅埃西亞文              | hr            |
| 匈牙利文             | hu            |
| 義大利文               | it            |
| 日文              | ja            |
| 坎那達文               | kn            |
| 韓文                | ko            |
| 馬來亞拉姆文             | ml            |
| 馬拉提文               | mr            |
| 馬來文                 | ms            |
| 挪威文 (巴克摩)      | nb            |
| 荷蘭文                 | nl            |
| 旁遮普文               | pa            |
| 波蘭文                | pl            |
| 葡萄牙文 - 巴西   | pt-br         |
| 葡萄牙文 - 葡萄牙 | pt-pt         |
| 羅馬尼亞文              | ro            |
| 俄文               | ru            |
| 斯洛伐克文                | sk            |
| 瑞典文               | sv            |
| 坦米爾文                 | ta            |
| 特拉古文                | te            |
| 泰文                  | th            |
| 土耳其文               | tr            |
| 中文 - 簡體  | zh-hans       |
| 中文 - 繁體 | zh-hant       |
