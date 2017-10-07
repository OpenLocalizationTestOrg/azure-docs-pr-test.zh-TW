---
title: "aaaAzure AD v2 ASP.NET Web 伺服器快速入門-測試 |Microsoft 文件"
description: "使用 OpenID Connect 標準，搭配傳統網頁瀏覽器型應用程式，在 ASP.NET 方案上實作 Microsoft 登入"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 99c7525b9146605142180962fc2a61b3c953c064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>測試您的程式碼

按`F5`toorun Visual Studio 中的專案。 hello 瀏覽器會開啟並引導您太*http://localhost: {port}* ，您會看到 hello*使用 Microsoft 登入* 按鈕。 請繼續進行，然後按一下它 toosign 中。

當您準備好 tootest，使用工作或學校 (Azure Active Directory) 或個人 （live.com、 outlook.com） 帳戶 toosign 中。 

![[使用 Microsoft 登入] 瀏覽器視窗](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![[使用 Microsoft 登入] 瀏覽器視窗](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a>預期的結果
登入之後 hello 使用者是網站的您，也就是網站的 hello hello Microsoft 應用程式註冊入口網站中您的應用程式的註冊資訊中所指定的 HTTPS URL 重新導向的 toohello 首頁。 此頁面現在會顯示*Hello {User}*和連結 toosign 外，以及連結 toosee hello 使用者宣告 – 這是連結 toohello 授權控制站之前建立。

### <a name="see-users-claims"></a>查看使用者的宣告
選取 hello 超連結 toosee hello 使用者的宣告。 這會導致您 toohello 控制器和檢視才會進行驗證的可用 toousers。

#### <a name="expected-results"></a>預期的結果
 您應該會看到包含 hello 的 hello 登入使用者的基本屬性的資料表：

| 屬性 | 值 | 描述|
|---|---|---|
| 名稱 | {使用者完整名稱} | hello 使用者的名字和姓氏
|使用者名稱 | <span>user@domain.com</span>| 用 tooidentify hello 登入使用者的 hello 使用者名稱
| 主旨| {主體}|字串 toouniquely hello web 識別 hello 使用者登入|
| 租用戶識別碼| {Guid}| A *guid* toouniquely 代表 hello 使用者的 Azure Active Directory 組織。|

此外，您也會看到一個表格，其中包含驗證要求中包括的所有使用者宣告。 如需識別碼權杖中所有宣告的清單和說明，請參閱這篇[文章]：(https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "識別碼權杖的宣告清單")。


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a>對具有 *[Authorize]* 屬性 (選用) 的方法進行存取測試
在此步驟中，您將測試存取 hello 驗證控制器匿名使用者的身分：<br/>
選取 hello 連結 toosign 外 hello 使用者和 hello 完成登出程序。<br/>
現在您的瀏覽器中輸入 http://localhost: {port} / 驗證 tooaccess 您 hello 受保護的控制器`[Authorize]`屬性

#### <a name="expected-results"></a>預期的結果
您應該會收到 hello 提示要求您 tooauthenticate toosee hello 檢視。

## <a name="additional-information"></a>其他資訊

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a>保護您的整個網站
tooprotect 整個網站，新增 hello`AuthorizeAttribute`太`GlobalFilters`中`Global.asax``Application_Start`方法：

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> **如何從 tooyour 應用程式中只能有一個組織 toosign toorestrict 使用者**

> 根據預設，個人帳戶 （包括 outlook.com、 live.com 和其他項目），以及從任何的公司或組織與 Azure Active Directory 整合的公司及學校帳戶可以登入 tooyour 應用程式。 

> 如果您希望您的應用程式 tooaccept 登入從只有一個 Azure Active Directory 組織，取代 hello`Tenant`中的參數*web.config*從`Common`hello 組織 – toohello 租用戶名稱範例中，*contoso.onmicrosoft.com*。在這之後，變更 hello`ValidateIssuer`引數中的您*OWIN 啟動 「 類別*太`true`。

> tooallow 一份特定組織，使用者設定`ValidateIssuer`tootrue 並用 hello`ValidIssuers`參數 toospecify 組織的清單。

> 另一個選項是使用 IssuerValidator 參數 toovalidate hello 簽發者 tooimplement 的自訂方法。 如需 `TokenValidationParameters` 的詳細資訊，請參閱[這篇 ](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN 文章") MSDN 文章。

