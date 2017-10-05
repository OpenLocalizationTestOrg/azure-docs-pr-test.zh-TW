---
title: "使用者介面 (UI) 自訂 - Azure AD B2C | Microsoft Docs"
description: "有關 Azure Active Directory B2C 中的使用者介面 (UI) 自訂功能的主題"
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
ms.openlocfilehash: 122fa997ea11b369aae3c59edf0043ab19d21aea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-customize-the-azure-ad-b2c-user-interface-ui"></a><span data-ttu-id="a70ef-103">Azure Active Directory B2C：自訂 Azure AD B2C 使用者介面 (UI)</span><span class="sxs-lookup"><span data-stu-id="a70ef-103">Azure Active Directory B2C: Customize the Azure AD B2C user interface (UI)</span></span>

<span data-ttu-id="a70ef-104">使用者經驗是客戶面向應用程式中最重要的。</span><span class="sxs-lookup"><span data-stu-id="a70ef-104">User experience is paramount in a customer facing application.</span></span>  <span data-ttu-id="a70ef-105">運用品牌外觀及風格來打造使用者經驗，從而擴大您的客戶群。</span><span class="sxs-lookup"><span data-stu-id="a70ef-105">Grow your customer base by crafting user experiences with the look and feel of your brand.</span></span> <span data-ttu-id="a70ef-106">Azure Active Directory B2C (Azure AD B2C) 可讓您以精準的像素控制來自訂註冊、登入、設定檔編輯和密碼重設頁面。</span><span class="sxs-lookup"><span data-stu-id="a70ef-106">Azure Active Directory B2C (Azure AD B2C) lets you customize sign-up, sign-in, profile editing, and password reset pages with pixel-perfect control.</span></span>

> [!NOTE]
> <span data-ttu-id="a70ef-107">本文中所述的網頁 UI 自訂功能並不適用於唯登入原則、其伴隨的密碼重設頁面，以及驗證電子郵件。</span><span class="sxs-lookup"><span data-stu-id="a70ef-107">The page UI customization feature described in this article does not apply to the sign-in only policy, its accompanying password reset page, and verification emails.</span></span>  <span data-ttu-id="a70ef-108">反之，這些功能會使用[公司品牌功能](../active-directory/active-directory-add-company-branding.md)。</span><span class="sxs-lookup"><span data-stu-id="a70ef-108">These features use the [company branding feature](../active-directory/active-directory-add-company-branding.md) instead.</span></span>
>

<span data-ttu-id="a70ef-109">本文章涵蓋下列主題：</span><span class="sxs-lookup"><span data-stu-id="a70ef-109">This article covers the following topics:</span></span>

* <span data-ttu-id="a70ef-110">頁面 UI 自訂功能。</span><span class="sxs-lookup"><span data-stu-id="a70ef-110">The page UI customization feature.</span></span>
* <span data-ttu-id="a70ef-111">用於將 HTML 內容上傳至 Azure Blob 儲存體，以搭配使用頁面 UI 自訂功能的工具。</span><span class="sxs-lookup"><span data-stu-id="a70ef-111">A tool for uploading HTML content to Azure Blob Storage for use with the page UI customization feature.</span></span>
* <span data-ttu-id="a70ef-112">您可以使用階層式樣式表 (CSS) 來進行自訂的 Azure AD B2C 所使用之 UI 元素。</span><span class="sxs-lookup"><span data-stu-id="a70ef-112">The UI elements used by Azure AD B2C that you can customize using Cascading Style Sheets (CSS).</span></span>
* <span data-ttu-id="a70ef-113">執行這項功能時的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="a70ef-113">Best practices when exercising this feature.</span></span>

## <a name="the-page-ui-customization-feature"></a><span data-ttu-id="a70ef-114">頁面 UI 自訂功能</span><span class="sxs-lookup"><span data-stu-id="a70ef-114">The page UI customization feature</span></span>

<span data-ttu-id="a70ef-115">您可以自訂客戶註冊、登入、密碼重設及設定檔編輯頁面的外觀和風格 (藉由設定 [原則](active-directory-b2c-reference-policies.md))。</span><span class="sxs-lookup"><span data-stu-id="a70ef-115">You can customize the look and feel of customer sign-up, sign-in, password reset, and profile-editing pages (by configuring [policies](active-directory-b2c-reference-policies.md)).</span></span> <span data-ttu-id="a70ef-116">客戶在您的應用程式與 Azure AD B2C 所提供的頁面之間瀏覽時，將會有順暢的體驗。</span><span class="sxs-lookup"><span data-stu-id="a70ef-116">Your customers get a seamless experience when navigating between your application and pages served by Azure AD B2C.</span></span>

<span data-ttu-id="a70ef-117">不同於 UI 選項的其他服務，Azure AD B2C 會使用簡單且現代的方法來自訂 UI。</span><span class="sxs-lookup"><span data-stu-id="a70ef-117">Unlike other services where UI options, Azure AD B2C uses a simple and modern approach to UI customization.</span></span>

<span data-ttu-id="a70ef-118">運作方式如下：Azure AD B2C 會在客戶的瀏覽器中執行程式碼並使用稱為[跨原始資源共用 (CORS)](http://www.w3.org/TR/cors/) 的新式方法。</span><span class="sxs-lookup"><span data-stu-id="a70ef-118">Here's how it works: Azure AD B2C runs code in your customer's browser and uses a modern approach called [Cross-Origin Resource Sharing (CORS)](http://www.w3.org/TR/cors/).</span></span>  <span data-ttu-id="a70ef-119">在執行階段中，會從您在原則中指定的 URL 載入內容。</span><span class="sxs-lookup"><span data-stu-id="a70ef-119">At run-time, content is loaded from a URL that you specify in a policy.</span></span> <span data-ttu-id="a70ef-120">您可以對不同的頁面指定不同的 URL。</span><span class="sxs-lookup"><span data-stu-id="a70ef-120">You can specify different URLs for different pages.</span></span> <span data-ttu-id="a70ef-121">從您 URL 載入的內容與從 Azure AD B2C 插入的 HTML 片段合併之後，就會向您的客戶顯示頁面。</span><span class="sxs-lookup"><span data-stu-id="a70ef-121">After content loaded from your URL is merged with an HTML fragment inserted from Azure AD B2C, the page is displayed to your customer.</span></span> <span data-ttu-id="a70ef-122">您只需要：</span><span class="sxs-lookup"><span data-stu-id="a70ef-122">All you need to do is:</span></span>

1. <span data-ttu-id="a70ef-123">建立格式正確的 HTML5 內容，其中的空白 `<div id="api"></div>` 元素位於 `<body>` 中的某處。</span><span class="sxs-lookup"><span data-stu-id="a70ef-123">Create well-formed HTML5 content with an empty `<div id="api"></div>` element located somewhere in the `<body>`.</span></span> <span data-ttu-id="a70ef-124">這個元素會標記插入 Azure AD B2C 內容的地方。</span><span class="sxs-lookup"><span data-stu-id="a70ef-124">This element marks where the Azure AD B2C content is inserted.</span></span>
1. <span data-ttu-id="a70ef-125">將您的內容裝載於 HTTPS 端點 (允許 CORS)。</span><span class="sxs-lookup"><span data-stu-id="a70ef-125">Host your content on an HTTPS endpoint (with CORS allowed).</span></span> <span data-ttu-id="a70ef-126">請注意，設定 CORS 時，必須同時啟用 GET 和 OPTIONS 要求方法。</span><span class="sxs-lookup"><span data-stu-id="a70ef-126">Note both GET and OPTIONS request methods must be enabled when configuring CORS.</span></span>
1. <span data-ttu-id="a70ef-127">使用 CSS 為 Azure AD B2C 所插入的 UI 項目設定樣式。</span><span class="sxs-lookup"><span data-stu-id="a70ef-127">Use CSS to style the UI elements that Azure AD B2C inserts.</span></span>

### <a name="a-basic-example-of-customized-html"></a><span data-ttu-id="a70ef-128">自訂 HTML 的基本範例</span><span class="sxs-lookup"><span data-stu-id="a70ef-128">A basic example of customized HTML</span></span>

<span data-ttu-id="a70ef-129">下列範例是可用來測試此功能的最基本 HTML 內容。</span><span class="sxs-lookup"><span data-stu-id="a70ef-129">The following example is the most basic HTML content that you can use to test this capability.</span></span> <span data-ttu-id="a70ef-130">請使用[協助程式工具](active-directory-b2c-reference-ui-customization-helper-tool.md)，在 Azure Blob 儲存體上傳和設定此內容。</span><span class="sxs-lookup"><span data-stu-id="a70ef-130">Use the [helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) to upload and configure this content on your Azure Blob storage.</span></span> <span data-ttu-id="a70ef-131">接著，您可以確認每個頁面上的無風格基本按鈕和表單欄位是否會顯示且功能正常。</span><span class="sxs-lookup"><span data-stu-id="a70ef-131">You can then verify that the basic, non-stylized buttons & form fields on each page are displayed and functional.</span></span>

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

## <a name="test-out-the-ui-customization-feature"></a><span data-ttu-id="a70ef-132">測試 UI 自訂功能</span><span class="sxs-lookup"><span data-stu-id="a70ef-132">Test out the UI customization feature</span></span>

<span data-ttu-id="a70ef-133">想要使用我們的範例 HTML 和 CSS 內容來嘗試 UI 自訂功能嗎？</span><span class="sxs-lookup"><span data-stu-id="a70ef-133">Want to try out the UI customization feature by using our sample HTML and CSS content?</span></span>  <span data-ttu-id="a70ef-134">我們提供了[協助程式工具](active-directory-b2c-reference-ui-customization-helper-tool.md)，讓您上傳範例內容，並在您的 Azure Blob 儲存體帳戶上進行設定。</span><span class="sxs-lookup"><span data-stu-id="a70ef-134">We've provided you [a helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) that uploads and configures sample content on your Azure Blob storage.</span></span>

> [!NOTE]
> <span data-ttu-id="a70ef-135">您可以將 UI 內容裝載於任何地方︰Web 伺服器、CDN、AWS S3、檔案共用系統等。只要內容是裝載在公開的 HTTPS 端點並啟用 CORS 就行。</span><span class="sxs-lookup"><span data-stu-id="a70ef-135">You can host your UI content anywhere: on web servers, CDNs, AWS S3, file sharing systems, etc. As long as the content is hosted on a publicly available HTTPS endpoint with CORS enabled, you are good to go.</span></span> <span data-ttu-id="a70ef-136">我們使用 Azure Blob 儲存體只是為了示範。</span><span class="sxs-lookup"><span data-stu-id="a70ef-136">We are using Azure Blob storage for illustrative purposes only.</span></span>
>

## <a name="the-ui-fragments-embedded-by-azure-ad-b2c"></a><span data-ttu-id="a70ef-137">Azure AD B2C 內嵌的 UI 片段</span><span class="sxs-lookup"><span data-stu-id="a70ef-137">The UI fragments embedded by Azure AD B2C</span></span>

<span data-ttu-id="a70ef-138">下列各節會列出 Azure AD B2C 合併至 `<div id="api"></div>` 元素 (位於您的內容中) 的 HTML5 片段範例。</span><span class="sxs-lookup"><span data-stu-id="a70ef-138">The following sections list the HTML5 fragments that Azure AD B2C merges into the `<div id="api"></div>` element located in your content.</span></span> <span data-ttu-id="a70ef-139">**請勿將這些片段插入 HTML 5 內容中。**</span><span class="sxs-lookup"><span data-stu-id="a70ef-139">**Do not insert these fragments in your HTML 5 content.**</span></span> <span data-ttu-id="a70ef-140">Azure AD B2C 服務會在執行階段插入。</span><span class="sxs-lookup"><span data-stu-id="a70ef-140">The Azure AD B2C service inserts them in at run-time.</span></span> <span data-ttu-id="a70ef-141">設計您的階層式樣式表 (CSS) 時，請使用這些片段作為參考。</span><span class="sxs-lookup"><span data-stu-id="a70ef-141">Use these fragments as a reference when designing your own Cascading Style Sheets (CSS).</span></span>

### <a name="fragment-inserted-into-the-identity-provider-selection-page"></a><span data-ttu-id="a70ef-142">插入「識別提供者選取頁面」中的片段</span><span class="sxs-lookup"><span data-stu-id="a70ef-142">Fragment inserted into the "Identity provider selection page"</span></span>

<span data-ttu-id="a70ef-143">此頁面包含使用者可以在註冊或登入期間選擇的身分識別提供者清單。</span><span class="sxs-lookup"><span data-stu-id="a70ef-143">This page contains a list of identity providers that the user can choose from during sign-up or sign-in.</span></span> <span data-ttu-id="a70ef-144">這些按鈕包括社交識別提供者 (如 Facebook 和 Google+) 或本機帳戶 (以電子郵件地址或使用者名稱作為基礎)。</span><span class="sxs-lookup"><span data-stu-id="a70ef-144">These buttons include social identity providers such as Facebook and Google+, or local accounts (based on email address or user name).</span></span>

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

### <a name="fragment-inserted-into-the-local-account-sign-up-page"></a><span data-ttu-id="a70ef-145">插入「本機帳戶註冊頁面」中的片段</span><span class="sxs-lookup"><span data-stu-id="a70ef-145">Fragment inserted into the "Local account sign-up page"</span></span>

<span data-ttu-id="a70ef-146">此頁面包含的表單，可供以電子郵件地址或使用者名稱作為基礎的本機帳戶註冊。</span><span class="sxs-lookup"><span data-stu-id="a70ef-146">This page contains a form for local account sign-up based on an email address or a user name.</span></span> <span data-ttu-id="a70ef-147">此表單可以包含不同的輸入控制項，例如文字輸入方塊、密碼輸入方塊、選項按鈕、單選下拉式清單方塊和多選核取方塊。</span><span class="sxs-lookup"><span data-stu-id="a70ef-147">The form can contain different input controls such as text input box, password entry box, radio button, single-select drop-down boxes, and multi-select check boxes.</span></span>

```HTML
<div id="api" data-name="SelfAsserted">
    <div class="intro">
        <p>Create your account by providing the following details</p>
    </div>

    <div id="attributeVerification">
        <div class="errorText" id="passwordEntryMismatch" style="display: none;">The password entry fields do not match. Please enter the same password in both fields and try again.</div>
        <div class="errorText" id="requiredFieldMissing" style="display: none;">A required field is missing. Please fill out all required fields and try again.</div>
        <div class="errorText" id="fieldIncorrect" style="display: none;">One or more fields are filled out incorrectly. Please check your entries and try again.</div>
        <div class="errorText" id="claimVerificationServerError" style="display: none;"></div>
        <div class="attr" id="attributeList">
            <ul>
                <li>
                    <div class="attrEntry validate">
                        <div>
                            <div class="verificationInfoText" id="email_intro" style="display: inline;">Verification is necessary. Please click Send button.</div>
                            <div class="verificationInfoText" id="email_info" style="display:none">Verification code has been sent to your inbox. Please copy it to the input box below.</div>
                            <div class="verificationSuccessText" id="email_success" style="display:none">E-mail address verified. You can now continue.</div>
                            <div class="verificationErrorText" id="email_fail_retry" style="display:none">Incorrect code, try again.</div>
                            <div class="verificationErrorText" id="email_fail_no_retry" style="display:none">Exceeded number of retries you need to send new code.</div>
                            <div class="verificationErrorText" id="email_fail_server" style="display:none">Server error, please try again</div>
                            <div class="verificationErrorText" id="email_incorrect_format" style="display:none">Incorect format.</div>
                        </div>

                    <div class="helpText show">This information is required</div>
                        <label>Email</label>
                        <input id="email" class="textInput" type="text" placeholder="Email" required="" autofocus=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Email address that can be used to contact you.');" class="tiny">What is this?</a>

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
                        <div class="helpText">8-16 characters, containing 3 out of 4 of the following: Lowercase characters, uppercase characters, digits (0-9), and one or more of the following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ " ( ) ; .This information is required</div>
                        <label>Enter password</label>
                        <input id="password" class="textInput" type="password" placeholder="Enter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title="8-16 characters, containing 3 out of 4 of the following: Lowercase characters, uppercase characters, digits (0-9), and one or more of the following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ &quot; ( ) ; ." required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Enter password');" class="tiny">What is this?</a>
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
                        <input id="postalCode" class="textInput" type="text" placeholder="Zip code" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('The postal code of your address.');" class="tiny">What is this?</a>
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

### <a name="fragment-inserted-into-the-social-account-sign-up-page"></a><span data-ttu-id="a70ef-148">插入「社交帳戶註冊頁面」中的片段</span><span class="sxs-lookup"><span data-stu-id="a70ef-148">Fragment inserted into the ""Social account sign-up page"</span></span>

<span data-ttu-id="a70ef-149">在使用社交識別提供者 (例如 Facebook 或 Google+) 的現有帳戶註冊時，可能會顯示此頁面。</span><span class="sxs-lookup"><span data-stu-id="a70ef-149">This page may appear when signing up using an existing account from a social identity provider such as Facebook or Google+.</span></span>  <span data-ttu-id="a70ef-150">必須向使用註冊表單之使用者收集其他資訊時需要使用它。</span><span class="sxs-lookup"><span data-stu-id="a70ef-150">It is used when additional information must be collected from the end user using a sign-up form.</span></span> <span data-ttu-id="a70ef-151">此頁面類似於本機帳戶註冊頁面 (如前一節所示)，但密碼輸入欄位除外。</span><span class="sxs-lookup"><span data-stu-id="a70ef-151">This page is similar to the local account sign-up page (shown in the previous section) with the exception of the password entry fields.</span></span>

### <a name="fragment-inserted-into-the-unified-sign-up-or-sign-in-page"></a><span data-ttu-id="a70ef-152">插入「統一註冊或登入頁面」中的片段</span><span class="sxs-lookup"><span data-stu-id="a70ef-152">Fragment inserted into the "Unified sign-up or sign-in page"</span></span>

<span data-ttu-id="a70ef-153">此頁面可處理客戶的註冊和登入，這些客戶可使用社交識別提供者 (例如 Facebook 或 Google+) 或本機帳戶。</span><span class="sxs-lookup"><span data-stu-id="a70ef-153">This page handles both sign-up & sign-in of customers, who can use social identity providers such as Facebook or Google+, or local accounts.</span></span>

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

### <a name="fragment-inserted-into-the-multi-factor-authentication-page"></a><span data-ttu-id="a70ef-154">插入「多重要素驗證頁面」中的片段</span><span class="sxs-lookup"><span data-stu-id="a70ef-154">Fragment inserted into the "Multi-factor authentication page"</span></span>

<span data-ttu-id="a70ef-155">在此頁面上，使用者可以在註冊或登入期間驗證其電話號碼 (使用文字或語音)。</span><span class="sxs-lookup"><span data-stu-id="a70ef-155">On this page, users can verify their phone numbers (using text or voice) during sign-up or sign-in.</span></span>

```HTML
<div id="api" data-name="Phonefactor">
    <div id="phonefactor_initial">
        <div class="intro">
            <p>Enter a number below that we can send a code via SMS or phone to authenticate you.</p>
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

### <a name="fragment-inserted-into-the-error-page"></a><span data-ttu-id="a70ef-156">插入「錯誤頁面」中的片段</span><span class="sxs-lookup"><span data-stu-id="a70ef-156">Fragment inserted into the ""Error page"</span></span>

```HTML
<div id="api" class="error-page-content" data-name="GlobalException">
    <h2>Sorry, but we're having trouble signing you in.</h2>
    <div class="error-page-help">We track these errors automatically, but if the problem persists feel free to contact us. In the meantime, please try again.</div>
    <div class="error-page-messagedetails">Your administrator hasn't provided any contact details.</div>
    <div class="error-page-messagedetails">
        <div class="error-page-correlationid">Correlation ID:1c4f0397-c6e4-4afe-bf74-42f488f2f15f</div>
        <div>Timestamp:2015-09-14 23:22:35Z</div>
        <div class="error-page-detail">AADB2C90065: A B2C client-side error 'Access is denied.' has occurred requesting the remote resource.</div>
    </div>
</div>
```

## <a name="localizing-your-html-content"></a><span data-ttu-id="a70ef-157">將 HTML 內容當地語系化</span><span class="sxs-lookup"><span data-stu-id="a70ef-157">Localizing your HTML content</span></span>

<span data-ttu-id="a70ef-158">您可以開啟[「語言自訂」](active-directory-b2c-reference-language-customization.md)，將 HTML 內容當地語系化。</span><span class="sxs-lookup"><span data-stu-id="a70ef-158">You can localize your HTML content by turning on ['Language customization'](active-directory-b2c-reference-language-customization.md).</span></span>  <span data-ttu-id="a70ef-159">啟用此功能會讓 Azure AD B2C 將 Open ID Connect 參數 `ui-locales` 轉送給端點。</span><span class="sxs-lookup"><span data-stu-id="a70ef-159">Enabling this feature allows Azure AD B2C to forward the Open ID Connect parameter, `ui-locales`, to your endpoint.</span></span>  <span data-ttu-id="a70ef-160">內容伺服器可以使用這個參數來提供語言特定的自訂 HTML 頁面。</span><span class="sxs-lookup"><span data-stu-id="a70ef-160">Your content server can use this parameter to provide customized HTML pages that are language-specific.</span></span>

## <a name="things-to-remember-when-building-your-own-content"></a><span data-ttu-id="a70ef-161">建置自己的內容時的注意事項</span><span class="sxs-lookup"><span data-stu-id="a70ef-161">Things to remember when building your own content</span></span>

<span data-ttu-id="a70ef-162">如果您打算使用頁面 UI 自訂功能，請檢閱以下最佳做法：</span><span class="sxs-lookup"><span data-stu-id="a70ef-162">If you are planning to use the page UI customization feature, review the following best practices:</span></span>

* <span data-ttu-id="a70ef-163">請勿複製 Azure AD B2C 的預設內容來嘗試修改。</span><span class="sxs-lookup"><span data-stu-id="a70ef-163">Don't copy the Azure AD B2C's default content and attempt to modify it.</span></span> <span data-ttu-id="a70ef-164">最好是從頭建置您的 HTML5 內容，將預設範本當作參考即可。</span><span class="sxs-lookup"><span data-stu-id="a70ef-164">It is best to build your HTML5 content from scratch and to use default content as reference.</span></span>
* <span data-ttu-id="a70ef-165">基於安全性理由，我們不允許您在內容中包含任何 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="a70ef-165">For security reasons, we don't allow you to include any JavaScript in your content.</span></span> <span data-ttu-id="a70ef-166">您所需的大多數功能應可立即使用。</span><span class="sxs-lookup"><span data-stu-id="a70ef-166">Most of what you need should be available out of the box.</span></span> <span data-ttu-id="a70ef-167">如果沒有，請使用 [User Voice (使用者心聲)](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) 來要求新功能。</span><span class="sxs-lookup"><span data-stu-id="a70ef-167">If not, use [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) to request new functionality.</span></span>
* <span data-ttu-id="a70ef-168">支援的瀏覽器版本︰</span><span class="sxs-lookup"><span data-stu-id="a70ef-168">Supported browser versions:</span></span>
  * <span data-ttu-id="a70ef-169">Internet Explorer 11、10、Edge</span><span class="sxs-lookup"><span data-stu-id="a70ef-169">Internet Explorer 11, 10, Edge</span></span>
  * <span data-ttu-id="a70ef-170">對 Internet Explorer 9、8 提供有限支援</span><span class="sxs-lookup"><span data-stu-id="a70ef-170">Limited support for Internet Explorer 9, 8</span></span>
  * <span data-ttu-id="a70ef-171">Google Chrome 42.0 和更新版本</span><span class="sxs-lookup"><span data-stu-id="a70ef-171">Google Chrome 42.0 and above</span></span>
  * <span data-ttu-id="a70ef-172">Mozilla Firefox 38.0 和更新版本</span><span class="sxs-lookup"><span data-stu-id="a70ef-172">Mozilla Firefox 38.0 and above</span></span>
