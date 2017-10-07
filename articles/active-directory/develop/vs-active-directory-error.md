---
title: "aaaHow toodiagnose 錯誤以 hello Azure Active Directory 連線精靈"
description: "hello active directory 連線精靈偵測到不相容的驗證類型"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: dd89ea63-4e45-4da1-9642-645b9309670a
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/05/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: f71c5b41457c0c8db05042e8d5f723e58ad11844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="diagnosing-errors-with-hello-azure-active-directory-connection-wizard"></a>診斷錯誤以 hello Azure Active Directory 連線精靈
偵測先前的驗證程式碼，時發生 hello 精靈偵測到不相容的驗證類型。   

## <a name="what-is-being-checked"></a>檢查什麼？
**注意：** toocorrectly 偵測先前的驗證程式碼專案中，必須建置 hello 專案。  如果遇到這個錯誤，且您的專案中沒有先前的驗證碼，請重建並再試一次。

### <a name="project-types"></a>專案類型
hello 精靈會檢查您正在開發，它可以將 hello 正確的驗證邏輯插入 hello 專案的專案 hello 類型。  如果沒有任何衍生自的控制站`ApiController`hello 專案視為 WebAPI 專案 hello 專案中。  如果沒有衍生自的控制器`MVC.Controller`hello 專案視為 MVC 專案 hello 專案中。  Hello 精靈不支援任何其他項目。

### <a name="compatible-authentication-code"></a>相容的驗證碼
hello 精靈也會檢查的先前設定使用 hello 精靈或 hello 精靈與相容的驗證設定。  如果所有設定都都存在，就會被視為可重新進入的情況下，，和 hello 精靈隨即開啟顯示 hello 設定。  如果只有部分 hello 設定存在，則會視為錯誤案例。

在 MVC 專案中，hello 精靈會檢查任何 hello 遵循因 hello 精靈的先前使用的設定：

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

此外，hello 精靈會檢查任何 hello 下列 Web API 專案時，源自 hello 精靈的先前使用的設定：

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a>不相容的驗證碼
最後，hello 精靈會嘗試驗證程式碼的已使用舊版 Visual Studio 的 toodetect 版本。 如果收到此錯誤，表示您的專案包含不相容的驗證類型。 hello 精靈偵測到舊版的 Visual Studio 中的下列類型的驗證 hello:

* Windows 驗證 
* 個別使用者帳戶 
* 組織帳戶 

toodetect MVC 專案中的 Windows 驗證，hello 精靈會尋找 hello`authentication`項目從您**web.config**檔案。

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

在 Web API 專案 toodetect Windows 驗證 hello 精靈會尋找 hello`IISExpressWindowsAuthentication`從您的專案項目**.csproj**檔案：

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

toodetect 個別使用者帳戶驗證，hello 精靈會尋找 hello 封裝元素，從您**Packages.config**檔案。

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

toodetect 是舊的組織帳戶驗證形式，hello 精靈會檢查下列項目從 hello **web.config**:

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

toochange hello 的驗證類型，移除 hello 不相容的驗證類型，然後再次執行 hello 精靈。

如需詳細資訊，請參閱 [Azure AD 的驗證案例](active-directory-authentication-scenarios.md)。

#<a name="next-steps"></a>後續步驟
- [Azure AD 的驗證案例](active-directory-authentication-scenarios.md)