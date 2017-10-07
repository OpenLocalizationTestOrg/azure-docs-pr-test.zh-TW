---
title: "aaaHow toodelegate 使用者註冊和產品訂用帳戶"
description: "了解如何 toodelegate 使用者註冊和產品訂用帳戶 tooa 協力廠商在 Azure API 管理。"
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 8b7ad5ee-a873-4966-a400-7e508bbbe158
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 406648db2d2f37c4dcda466294726d331cc0551b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodelegate-user-registration-and-product-subscription"></a>如何 toodelegate 使用者註冊和產品訂用帳戶
委派可讓您 toouse 處理做為開發人員登在 /-註冊和訂用帳戶 tooproducts 您現有的網站而非在 hello 開發人員入口網站中的 toousing hello 內建功能。 這可讓您網站 tooown hello 的使用者資料，並在自訂的方式執行這些步驟的 hello 驗證。

## <a name="delegate-signin-up"> </a>委派開發人員登入和註冊
toodelegate 開發人員登入並註冊 tooyour 現有網站做為 hello 從 hello API 管理開發人員入口網站起始任何這類要求的進入點的網站必須 toocreate 特殊委派端點。

hello 最後的工作流程會如下所示：

1. 開發人員按一下 hello 登入或註冊連結在 hello API 管理開發人員入口網站
2. 瀏覽器會重新導向的 toohello 委派端點
3. 委派端點傳回 tooor 呈現 UI 詢問將使用者重新導向或註冊 toosign 中
4. 成功時，hello 使用者已重新導向後 toohello API 管理開發人員入口網站頁面從它們啟動

toobegin，讓我們第一次設定 API 管理 tooroute 會要求透過您委派的端點。 在 [hello API 管理發行者入口網站，按一下**安全性**然後按一下hello**委派**] 索引標籤。按一下 [hello] 核取方塊 tooenable 'Delegate 登入 （& s) 註冊'。

![Delegation page][api-management-delegation-signin-up]

* 決定哪些 hello 特殊委派端點 URL 會並進入 hello**委派端點 URL**欄位。 
* 在 hello**委派驗證金鑰**欄位中，輸入將會使用的 toocompute hello 要求的驗證 tooensure 的簽章提供 tooyou 確實來自 Azure API 管理的密碼。 您可以按一下 hello**產生**按鈕 toohave API 積存，隨機產生金鑰。

現在您需要 toocreate hello**委派端點**。 它有 tooperform 數個動作：

1. 在下列形式的 hello 收到的要求：
   
   > http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}
   > 
   > 
   
    Hello 登入 / 註冊案例的查詢參數：
   
   * **operation**：識別委派要求的類型 - 在此案例中只能是 **SignIn**
   * **returnUrl**: hello hello 使用者在登入或註冊連結的點選處的 hello 網頁的 URL
   * **salt**：特殊 salt 字串，用於計算安全性雜湊
   * **sig**： 用於比較 tooyour 自己計算的安全性雜湊 toobe 計算雜湊
2. 請確認該 hello 要求來自於 Azure API 管理 （選擇性，但強烈建議使用的安全性）
   
   * 計算字串 hello 為基礎的 hmac-sha512 雜湊**returnUrl**和**salt**查詢參數 ([下面提供的範例程式碼]):
     
     > HMAC(**salt** + '\n' + **returnUrl**)
     > 
     > 
   * 比較 hello hello 上面計算出雜湊 toohello 值**sig**查詢參數。 如果 hello 兩個雜湊相符，toohello 下一個步驟上移動，否則會拒絕 hello 要求。
3. 確認您收到登輸入/符號上的要求： hello**作業**查詢參數會設定得 「**SignIn**"。
4. 使用 UI 或註冊 toosign 中出現的 hello 使用者
5. 如果 hello 使用者註冊您的 toocreate 對應帳戶它們在 API 管理。 [建立使用者]以 hello API 管理 REST API。 當此情況下，確定您設定 hello 使用者識別碼 toohello 您使用者存放區中相同或 tooan 識別碼，您可以追蹤。
6. 當成功驗證 hello 使用者：
   
   * [要求的單一登入 (SSO) 權杖]透過 hello API 管理 REST API
   * 附加 returnUrl 查詢參數 toohello SSO URL 收到來自上述的 hello API 呼叫：
     
     > 例如，https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url 
     > 
     > 
   * 重新導向 hello 使用者 toohello 上面所產生的 URL

在加法 toohello **SignIn**作業，您也可以執行帳戶管理 hello 上一個步驟，並使用其中一個 hello 下列作業。

* **ChangePassword**
* **ChangeProfile**
* **CloseAccount**

您必須傳遞下列帳戶管理作業的查詢參數的 hello。

* **operation**：識別委派要求的類型 (ChangePassword、ChangeProfile 或 CloseAccount)
* **userId**: hello 帳戶 toomanage hello 使用者識別碼
* **salt**：特殊 salt 字串，用於計算安全性雜湊
* **sig**： 用於比較 tooyour 自己計算的安全性雜湊 toobe 計算雜湊

## <a name="delegate-product-subscription"> </a>委派產品訂閱
委派產品訂用帳戶的運作方式類似 toodelegating 使用者登入/總。 hello 最後的工作流程應如下所示：

1. 開發人員在 hello API 管理開發人員入口網站中選取產品，然後按一下 hello 訂閱 」 按鈕
2. 瀏覽器會重新導向的 toohello 委派端點
3. 委派端點會執行必要的產品訂用帳戶的步驟-這是總 tooyou，而且可能需要重新導向 tooanother 頁面 toorequest 帳單資訊、 詢問其他問題，或只儲存 hello 資訊並不需要任何使用者動作

hello 上的 tooenable hello 功能**委派**頁面上，按一下**委派產品訂閱**。

請確定 hello 委派端點執行下列動作的 hello:

1. 在下列形式的 hello 收到的要求：
   
   > *http://www.yourwebsite.com/apimdelegation?operation= {作業} （& s) productId = {產品 toosubscribe 至} （& s) userId = {提出要求的 user} & salt = {string} （& s) sig = {string}*
   > 
   > 
   
    Hello 產品訂閱案例的查詢參數：
   
   * **operation**：識別委派要求的類型。 產品訂用帳戶要求 hello 有效的選項為：
     * 「 訂閱 」: 指定產品要求 toosubscribe hello 使用者 tooa 提供識別碼 （請參閱下文）
     * 「 取消 」: 要求 toounsubscribe 產品中的使用者
     * 「 更新 」: 要求的 toorenew 的訂用帳戶 （例如可能即將到期的時間）
   * **productId**: hello 識別碼 hello 產品 hello 使用者要求來 toosubscribe
   * **userId**: hello hello 使用者針對 hello 要求識別碼
   * **salt**：特殊 salt 字串，用於計算安全性雜湊
   * **sig**： 用於比較 tooyour 自己計算的安全性雜湊 toobe 計算雜湊
2. 請確認該 hello 要求來自於 Azure API 管理 （選擇性，但強烈建議使用的安全性）
   
   * 計算字串 hello 為基礎的 hmac-sha512 **productId**， **userId**和**salt**查詢參數：
     
     > HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)
     > 
     > 
   * 比較 hello hello 上面計算出雜湊 toohello 值**sig**查詢參數。 如果 hello 兩個雜湊相符，toohello 下一個步驟上移動，否則會拒絕 hello 要求。
3. 執行根據 hello 類型中所要求任何的作業產品訂用帳戶處理**作業**-例如計費，取得進一步的問題，依此類推。
4. 在成功訂閱 hello 使用者 toohello 產品，在您身邊，訂閱 hello 使用者 toohello API 管理產品[呼叫 hello REST API 產品訂用帳戶]。

## <a name="delegate-example-code"> </a> 範例程式碼
這些程式碼範例顯示如何 tootake hello*委派驗證金鑰*hello 委派 hello 發行者入口網站畫面中設定、 toocreate 的 HMAC，然後使用 toovalidate hello 簽章，證明 hello hello 有效性傳回傳入的 Url。 相同的程式碼適用於 hello productId 和稍微修改的使用者識別碼 hello。

**C# 程式碼 toogenerate 的雜湊 returnUrl**

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature toosig query parameter
}
```

**NodeJS 的 returnUrl toogenerate 雜湊程式碼**

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature toosig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a>後續步驟
如需委派的詳細資訊，請參閱下列視訊的 hello。

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
[要求的單一登入 (SSO) 權杖]: http://go.microsoft.com/fwlink/?LinkId=507409
[建立使用者]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser
[呼叫 hello REST API 產品訂用帳戶]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO
[Next steps]: #next-steps
[下面提供的範例程式碼]: #delegate-example-code

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
