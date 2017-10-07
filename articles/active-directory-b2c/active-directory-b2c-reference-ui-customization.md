---
title: "使用者介面 (UI) 自訂 - Azure AD B2C | Microsoft Docs"
description: "在 hello 使用者介面 (UI) 的自訂功能在 Azure Active Directory B2C 的主題"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 99f5a391-5328-471d-a15c-a2fafafe233d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 04f8c5f1277f8d4409cd10971d22a0ebd2024785
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-customize-hello-azure-ad-b2c-user-interface-ui"></a>Azure Active Directory B2C： 自訂 hello Azure AD B2C 使用者介面 (UI)

使用者經驗是客戶面向應用程式中最重要的。  製作與 hello 的外觀與您的品牌的使用者經驗時，擴大客戶群。 Azure Active Directory B2C (Azure AD B2C) 可讓您以精準的像素控制來自訂註冊、登入、設定檔編輯和密碼重設頁面。

> [!NOTE]
> 只有原則登入 toohello、 其隨附的密碼重設頁面，以及驗證電子郵件，則不適用本文中所述的 hello 頁 UI 自訂功能。  這些功能會使用 hello[公司品牌功能](../active-directory/active-directory-add-company-branding.md)改為。
>

本文涵蓋下列主題中的 hello:

* hello 頁 UI 自訂功能。
* 用於上傳 HTML 內容 tooAzure Blob 儲存體，hello 頁 UI 自訂功能搭配使用的工具。
* 您可以使用階層式樣式表 (CSS) 來進行自訂的 Azure AD B2C 所使用的 hello UI 項目。
* 執行這項功能時的最佳做法。

## <a name="hello-page-ui-customization-feature"></a>hello 頁 UI 自訂功能

您可以自訂 hello 的外觀及客戶註冊、 登入密碼重設和設定檔編輯頁面 (藉由設定[原則](active-directory-b2c-reference-policies.md))。 客戶在您的應用程式與 Azure AD B2C 所提供的頁面之間瀏覽時，將會有順暢的體驗。

不同於其他 UI 選項，Azure AD B2C 使用簡單和現代要很接近 tooUI 自訂服務。

運作方式如下：Azure AD B2C 會在客戶的瀏覽器中執行程式碼並使用稱為[跨原始資源共用 (CORS)](http://www.w3.org/TR/cors/) 的新式方法。  在執行階段中，會從您在原則中指定的 URL 載入內容。 您可以對不同的頁面指定不同的 URL。 從您的 URL 載入的內容會與從 Azure AD B2C 插入的 HTML 片段合併之後，hello 頁面會顯示的 tooyour 客戶。 您只需要 toodo 是：

1. 建立具有空白內容語式正確的 HTML5`<div id="api"></div>`項目處 hello `<body>`。 此項目標記，插入 hello Azure AD B2C 內容的位置。
1. 將您的內容裝載於 HTTPS 端點 (允許 CORS)。 請注意，設定 CORS 時，必須同時啟用 GET 和 OPTIONS 要求方法。
1. 使用 CSS toostyle hello UI 項目，Azure AD B2C 插入。

### <a name="a-basic-example-of-customized-html"></a>自訂 HTML 的基本範例

下列範例中的 hello 是 hello 最基本的 HTML 內容，您可以使用 tootest 這項功能。 使用 hello [helper 工具](active-directory-b2c-reference-ui-customization-helper-tool.md)tooupload 和您的 Azure Blob 儲存體設定此內容。 接著，您可以確認 hello 基本的非稍許按鈕與每個頁面上的表單欄位會顯示並可運作。

```HTML
<!DOCTYPE html>
<html>
    <head>
        <title>!Add your title here!</title>
    </head>
    <body>
        <div id="api"></div>   <!-- Leave this element empty because Azure AD B2C will insert content here. -->
    </body>
</html>
```

## <a name="test-out-hello-ui-customization-feature"></a>Hello UI 自訂功能測試

使用我們的範例 HTML 和 CSS 內容想 tootry 出 hello UI 自訂功能？  我們提供了[協助程式工具](active-directory-b2c-reference-ui-customization-helper-tool.md)，讓您上傳範例內容，並在您的 Azure Blob 儲存體帳戶上進行設定。

> [!NOTE]
> 您可以將 UI 內容裝載於任何地方︰Web 伺服器、CDN、AWS S3、檔案共用系統等。只要 hello 內容裝載於公開可用的 HTTPS 端點以啟用 CORS 時，您都是很好的 toogo。 我們使用 Azure Blob 儲存體只是為了示範。
>

## <a name="hello-ui-fragments-embedded-by-azure-ad-b2c"></a>內嵌的 Azure AD B2C hello UI 片段

hello 下列各節列出 Azure AD B2C 合併至 hello 的 hello HTML5 片段`<div id="api"></div>`項目位於您的內容。 **請勿將這些片段插入 HTML 5 內容中。** hello Azure AD B2C 服務會在執行階段中插入。 設計您的階層式樣式表 (CSS) 時，請使用這些片段作為參考。

### <a name="fragment-inserted-into-hello-identity-provider-selection-page"></a>Hello 身分識別提供者選取項目頁面 」 所插入片段

此頁面包含一份 hello 使用者的提供者註冊或登入期間，可以選擇從身分識別。 這些按鈕包括社交識別提供者 (如 Facebook 和 Google+) 或本機帳戶 (以電子郵件地址或使用者名稱作為基礎)。

```HTML
<div id="api" data-name="IdpSelections">
    <div class="intro">
         <p>Sign up</p>
    </div>

    <div>
        <ul>
            <li>
                <button class="accountButton" id="FacebookExchange">Facebook</button>
            </li>
            <li>
                <button class="accountButton" id="GoogleExchange">Google+</button>
            </li>
            <li>
                <button class="accountButton" id="SignUpWithLogonEmailExchange">Email</button>
            </li>
        </ul>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-local-account-sign-up-page"></a>Hello 本機帳戶註冊頁面 」 所插入片段

此頁面包含的表單，可供以電子郵件地址或使用者名稱作為基礎的本機帳戶註冊。 hello 表單可以包含不同的輸入的控制項，例如文字輸入的方塊、 密碼輸入方塊、 選項按鈕、 單一選取下拉式清單方塊中和多重選取的核取方塊。

```HTML
<div id="api" data-name="SelfAsserted">
    <div class="intro">
        <p>Create your account by providing hello following details</p>
    </div>

    <div id="attributeVerification">
        <div class="errorText" id="passwordEntryMismatch" style="display: none;">hello password entry fields do not match. Please enter hello same password in both fields and try again.</div>
        <div class="errorText" id="requiredFieldMissing" style="display: none;">A required field is missing. Please fill out all required fields and try again.</div>
        <div class="errorText" id="fieldIncorrect" style="display: none;">One or more fields are filled out incorrectly. Please check your entries and try again.</div>
        <div class="errorText" id="claimVerificationServerError" style="display: none;"></div>
        <div class="attr" id="attributeList">
            <ul>
                <li>
                    <div class="attrEntry validate">
                        <div>
                            <div class="verificationInfoText" id="email_intro" style="display: inline;">Verification is necessary. Please click Send button.</div>
                            <div class="verificationInfoText" id="email_info" style="display:none">Verification code has been sent tooyour inbox. Please copy it toohello input box below.</div>
                            <div class="verificationSuccessText" id="email_success" style="display:none">E-mail address verified. You can now continue.</div>
                            <div class="verificationErrorText" id="email_fail_retry" style="display:none">Incorrect code, try again.</div>
                            <div class="verificationErrorText" id="email_fail_no_retry" style="display:none">Exceeded number of retries you need toosend new code.</div>
                            <div class="verificationErrorText" id="email_fail_server" style="display:none">Server error, please try again</div>
                            <div class="verificationErrorText" id="email_incorrect_format" style="display:none">Incorect format.</div>
                        </div>

                    <div class="helpText show">This information is required</div>
                        <label>Email</label>
                        <input id="email" class="textInput" type="text" placeholder="Email" required="" autofocus=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Email address that can be used toocontact you.');" class="tiny">What is this?</a>

                    <div class="buttons verify" claim_id="email">
                        <div id="email_ver_wait" class="working" style="display: none;"></div>
                            <label id="email_ver_input_label" for="email_ver_input" style="display: none;">Verification code</label>
                            <input id="email_ver_input" type="text" placeholder="Verification code" style="display:none">
                            <button id="email_ver_but_send" class="sendButton" type="button" style="display: inline;">Send verification code</button>
                            <button id="email_ver_but_verify" class="verifyButton" type="button" style="display:none">Verify code</button>
                            <button id="email_ver_but_resend" class="sendButton" type="button" style="display:none">Send new code</button>
                            <button id="email_ver_but_edit" class="editButton" type="button" style="display:none">Change e-mail</button>
                            <button id="email_ver_but_default" class="defaultButton" type="button" style="display:none">Default</button>
                        </div>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">8-16 characters, containing 3 out of 4 of hello following: Lowercase characters, uppercase characters, digits (0-9), and one or more of hello following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ " ( ) ; .This information is required</div>
                        <label>Enter password</label>
                        <input id="password" class="textInput" type="password" placeholder="Enter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title="8-16 characters, containing 3 out of 4 of hello following: Lowercase characters, uppercase characters, digits (0-9), and one or more of hello following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ &quot; ( ) ; ." required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Enter password');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"> This information is required</div>
                        <label>Reenter password</label>
                        <input id="reenterPassword" class="textInput" type="password" placeholder="Reenter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title=" " required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Reenter password');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">This information is required</div>
                        <label>Name</label>
                        <input id="displayName" class="textInput" type="text" placeholder="Name" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Your display name.');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>Gender</label>
                        <input id="extension_Gender_F" name="extension_Gender" type="radio" value="F" autofocus="">
                        <label for="extension_Gender_F">Female</label>
                        <input id="extension_Gender_M" name="extension_Gender" type="radio" value="M">
                        <label for="extension_Gender_M">Male</label>
                        <a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>Loyalty number</label>
                        <input id="extension_MemNum" class="textInput" type="text" placeholder="Loyalty number"><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Membership number');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>State</label>
                        <select class="dropdown_single" id="state">
                            <option style="display:none" disabled="disabled" value="placeholder" selected="">State</option>
                            <option value="WA">Washington</option>
                            <option value="NY">New York</option>
                            <option value="CA">California</option>
                        </select>
                        <a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Your residential state or province.');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">This information is required</div>
                        <label>Zip code</label>
                        <input id="postalCode" class="textInput" type="text" placeholder="Zip code" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('hello postal code of your address.');" class="tiny">What is this?</a>
                    </div>
                </li>
            </ul>
        </div>
        <div class="buttons"> <button id="continue" disabled="">Create</button> <button id="cancel">Cancel</button></div>
    </div>
    <div class="verifying-modal">
        <div class="preloader"> <img src="https://login.microsoftonline.com/static/img/win8loader.gif" alt="Please wait"></div>
        <div id="verifying_blurb"></div>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-social-account-sign-up-page"></a>片段插入 hello""社交帳戶註冊頁面"

在使用社交識別提供者 (例如 Facebook 或 Google+) 的現有帳戶註冊時，可能會顯示此頁面。  它必須從 hello 終端使用者使用註冊表單收集其他資訊時使用。 此頁面是類似 toohello 本機帳戶註冊頁面 （hello 前一節中所示），hello 密碼輸入欄位的 hello 例外狀況。

### <a name="fragment-inserted-into-hello-unified-sign-up-or-sign-in-page"></a>Hello 統一註冊或登入頁面 」 所插入片段

此頁面可處理客戶的註冊和登入，這些客戶可使用社交識別提供者 (例如 Facebook 或 Google+) 或本機帳戶。

```HTML
<div id="api" data-name="Unified">
        <div class="social" role="form">
               <div class="intro">
                       <h2>Sign in with your social account</h2>
               </div>
               <div class="options">
                       <div><button class="accountButton firstButton" id="MicrosoftAccountExchange" tabindex="1">msa</button></div>
                       <div><button class="accountButton" id="FacebookExchange" tabindex="1">fb</button></div>
               </div>
        </div>
        <div class="divider">
               <h2>OR</h2>
        </div>
        <div class="localAccount" role="form">
               <div class="intro">
                       <h2>Sign in with your existing account</h2>
               </div>
               <div class="error pageLevel" aria-hidden="true" style="display: none;">
                       <p role="alert"></p>
               </div>
               <div class="entry">
                       <div class="entry-item">
                               <label for="logonIdentifier">Email Address</label> 
                               <div class="error itemLevel" aria-hidden="true" style="display: none;">
                                      <p role="alert"></p>
                               </div>
                               <input type="email" id="logonIdentifier" name="LogonIdentifier" pattern="^[a-zA-Z0-9.!#$%&amp;’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$" placeholder="LogonIdentifier" value="" tabindex="1">
                       </div>
                       <div class="entry-item">
                               <div class="password-label"> <label for="password">Password</label><a id="forgotPassword" tabindex="2">Forgot your password?</a></div>
                               <div class="error itemLevel" aria-hidden="true" style="display: none;">
                                      <p role="alert"></p>
                               </div>
                               <input type="password" id="password" name="Password" placeholder="Password" tabindex="1">
                       </div>
                       <div class="working"></div>
                       <div class="buttons"> <button id="next" tabindex="1">Sign in</button> </div>
               </div>
               <div class="divider">
                       <h2>OR</h2>
               </div>
               <div class="create">
                       <p>Don't have an account?<a id="createAccount" tabindex="1">Sign up now</a> </p>
               </div>
        </div>
</div>
```

### <a name="fragment-inserted-into-hello-multi-factor-authentication-page"></a>Hello multi-factor authentication 頁面 」 所插入片段

在此頁面上，使用者可以在註冊或登入期間驗證其電話號碼 (使用文字或語音)。

```HTML
<div id="api" data-name="Phonefactor">
    <div id="phonefactor_initial">
        <div class="intro">
            <p>Enter a number below that we can send a code via SMS or phone tooauthenticate you.</p>
        </div>
        <div class="errorText" id="errorMessage" style="display:none"></div>
        <div class="phoneEntry" id="phoneEntry">
            <div class="phoneNumber">
                <select id="countryCode" style="display:inline-block">
                    <option value="+93">Afghanistan (+93)</option>
                    <!-- Not all country codes listed -->
                    <option value="+44">United Kingdom (+44)</option>
                    <option value="+1" selected="">United States (+1)</option>
                    <!-- Not all country codes listed -->
                </select>
            </div>
            <div class="phoneNumber">
                <input type="text" id="localNumber" style="display:inline-block" placeholder="Phone number">
            </div>
        </div>
        <div id="codeVerification" style="display:none">
            <div>
                <p>Enter your verification code below, or <button id="retryCode" class="textButton">send a new code</button></p>
                <input type="text" id="verificationCode" placeholder="Verification code">
            </div>
        </div>
        <div class="buttons">
            <button id="verifyCode" class="sendInitialCodeButton">Send Code</button>
            <button id="verifyPhone" style="display:inline-block">Call Me</button>
            <button id="cancel" style="display:inline-block">Cancel</button>
        </div>
    </div>
    <div class="dialing-modal">
        <div class="preloader"> <img src="https://login.microsoftonline.com/static/img/win8loader.gif" alt="Please wait"></div>
        <div id="dialing_blurb"></div><div id="dialing_number"></div>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-error-page"></a>Hello 」 錯誤頁面 」 所插入片段

```HTML
<div id="api" class="error-page-content" data-name="GlobalException">
    <h2>Sorry, but we're having trouble signing you in.</h2>
    <div class="error-page-help">We track these errors automatically, but if hello problem persists feel free toocontact us. In hello meantime, please try again.</div>
    <div class="error-page-messagedetails">Your administrator hasn't provided any contact details.</div>
    <div class="error-page-messagedetails">
        <div class="error-page-correlationid">Correlation ID:1c4f0397-c6e4-4afe-bf74-42f488f2f15f</div>
        <div>Timestamp:2015-09-14 23:22:35Z</div>
        <div class="error-page-detail">AADB2C90065: A B2C client-side error 'Access is denied.' has occurred requesting hello remote resource.</div>
    </div>
</div>
```

## <a name="localizing-your-html-content"></a>將 HTML 內容當地語系化

您可以開啟[「語言自訂」](active-directory-b2c-reference-language-customization.md)，將 HTML 內容當地語系化。  啟用這項功能可讓 Azure AD B2C tooforward hello 開啟連接的識別碼參數， `ui-locales`，tooyour 端點。  到內容伺服器可以使用這個語言特定的參數 tooprovide 自訂 HTML 網頁。

## <a name="things-tooremember-when-building-your-own-content"></a>建置您自己的內容時，項目 tooremember

如果您打算 toouse hello 頁 UI 自訂功能，請檢閱下列最佳作法的 hello:

* 不要複製 hello Azure AD B2C 的預設內容中，然後嘗試 toomodify 它。 它是最佳 toobuild 從平滑和 toouse 預設內容做為參考您 HTML5 的內容。
* 基於安全性理由，我們不允許您 tooinclude 任何在您的內容中的 JavaScript。 所需的大部分應該可以使用現成 hello。 如果沒有，請使用[User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) toorequest 新功能。
* 支援的瀏覽器版本︰
  * Internet Explorer 11、10、Edge
  * 對 Internet Explorer 9、8 提供有限支援
  * Google Chrome 42.0 和更新版本
  * Mozilla Firefox 38.0 和更新版本
