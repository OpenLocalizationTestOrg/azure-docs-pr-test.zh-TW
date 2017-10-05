---
title: "Azure API 管理中的頁面範本 | Microsoft Docs"
description: "了解如何使用「Azure API 管理」中的一組範本來自訂開發人員入口網站頁面的內容。"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: e57df269-1019-4b74-b74d-53155b809d59
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 7f9ef37a694bce786b6acaa428df83f0cb23c2dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="page-templates-in-azure-api-management"></a><span data-ttu-id="39a71-103">Azure API 管理中的頁面範本</span><span class="sxs-lookup"><span data-stu-id="39a71-103">Page templates in Azure API Management</span></span>
<span data-ttu-id="39a71-104">「Azure API 管理」可讓您使用一組可設定開發人員入口網站頁面內容的範本，來自訂那些頁面的內容。</span><span class="sxs-lookup"><span data-stu-id="39a71-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="39a71-105">使用這些範本時，您可以運用 [DotLiquid](http://dotliquidmarkup.org/) 語法和您選擇的編輯器 (例如 [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers))，以及一組提供的當地語系化[字串資源](api-management-template-resources.md#strings)、[字符資源](api-management-template-resources.md#glyphs)和[頁面控制項](api-management-page-controls.md)，依照您的想法自由靈活地設定頁面內容。</span><span class="sxs-lookup"><span data-stu-id="39a71-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="39a71-106">本節中的範本可讓您自訂開發人員入口網站中下列頁面的內容：登入、註冊及找不到頁面。</span><span class="sxs-lookup"><span data-stu-id="39a71-106">The templates in this section allow you to customize the content of the sign in, sign up, and page not found pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="39a71-107">登入</span><span class="sxs-lookup"><span data-stu-id="39a71-107">Sign in</span></span>](#SignIn)  
  
-   [<span data-ttu-id="39a71-108">註冊</span><span class="sxs-lookup"><span data-stu-id="39a71-108">Sign up</span></span>](#SignUp)  
  
-   [<span data-ttu-id="39a71-109">找不到頁面</span><span class="sxs-lookup"><span data-stu-id="39a71-109">Page not found</span></span>](#PageNotFound)  
  
> [!NOTE]
>  <span data-ttu-id="39a71-110">下列文件中包含範例預設範本，但範本可能會因持續進行的改善而有變更。</span><span class="sxs-lookup"><span data-stu-id="39a71-110">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="39a71-111">您可以瀏覽至想要的個別範本，來檢視開發人員入口網站中的即時預設範本。</span><span class="sxs-lookup"><span data-stu-id="39a71-111">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="39a71-112">如需有關使用範本的詳細資訊，請參閱[如何使用範本自訂 API 管理開發人員入口網站](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)。</span><span class="sxs-lookup"><span data-stu-id="39a71-112">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="39a71-113"><a name="SignIn"></a> 登入</span><span class="sxs-lookup"><span data-stu-id="39a71-113"><a name="SignIn"></a> Sign in</span></span>  
 <span data-ttu-id="39a71-114">「登入」範本可讓您自訂開發人員入口網站中的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="39a71-114">The **sign in** template allows you to customize the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="39a71-115">![登入頁面](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM 登入頁面開發人員入口網站範本")</span><span class="sxs-lookup"><span data-stu-id="39a71-115">![Sign In Page](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM Sign In Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="39a71-116">預設範本</span><span class="sxs-lookup"><span data-stu-id="39a71-116">Default template</span></span>  
  
```xml  
<h2 class="text-center">{% localized "SigninStrings|WebAuthenticationSigninTitle" %}</h2>  
{% if registrationEnabled == true %}  
<p class="text-center">{% localized "SigninStrings|WebAuthenticationNotAMember" %}</p>  
{% endif %}  
  
<div class="row center-block ap-idp-container">  
  <div class="col-md-6">  
    {% if registrationEnabled == true %}  
        <p>{% localized "SigninStrings|WebAuthenticationSigininWithPassword" %}</p>  
    <basic-SignIn></basic-SignIn>  
    {% endif %}  
  </div>  
  
    {% if registrationEnabled != true and providers.size == 0 %}  
        {% localized "ProviderInfoStrings|TextboxExternalIdentitiesDisabled" %}  
  {% else %}  
        {% if providers.size > 0 %}  
      <div class="col-md-6">  
            <div class="providers-list">  
                <p class="text-left">  
                {% if registrationEnabled == true %}  
                    {% localized "ProviderInfoStrings|TextboxExternalIdentitiesSigninInvitation" %}  
                {% else %}  
                    {% localized "ProviderInfoStrings|TextboxExternalIdentitiesSigninInvitationPrimary" %}  
                {% endif %}  
                </p>  
        <providers></providers>  
            </div>  
    </div>  
        {% endif %}  
    {% endif %}  
  
  {% if userRegistrationTermsEnabled == true %}  
    <div class="col-md-6">  
        <div id="terms" class="modal" role="dialog" tabindex="-1">  
            <div class="modal-dialog">  
                <div class="modal-content">  
                    <div class="modal-header">  
                        <h4 class="modal-title">{% localized "SigninResources|DialogHeadingTermsOfUse" %}</h4>  
                    </div>  
                    <div class="modal-body break-all">{{userRegistrationTerms}}</div>  
                    <div class="modal-footer">  
                        <button type="button" class="btn btn-default" data-dismiss="modal">{% localized "CommonStrings|ButtonLabelClose" %}</button>  
                    </div>  
                </div>  
            </div>  
        </div>  
        <p>{% localized "SigninResources|TextblockUserRegistrationTermsProvided" %}</p>  
    </div>  
    {% endif %}  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="39a71-117">控制</span><span class="sxs-lookup"><span data-stu-id="39a71-117">Controls</span></span>  
 <span data-ttu-id="39a71-118">此範本可能會使用下列[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="39a71-118">This template may  use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="39a71-119">basic-signin</span><span class="sxs-lookup"><span data-stu-id="39a71-119">basic-signin</span></span>](api-management-page-controls.md#basic-signin)  
  
-   [<span data-ttu-id="39a71-120">提供者</span><span class="sxs-lookup"><span data-stu-id="39a71-120">providers</span></span>](api-management-page-controls.md#providers)  
  
### <a name="data-model"></a><span data-ttu-id="39a71-121">資料模型</span><span class="sxs-lookup"><span data-stu-id="39a71-121">Data model</span></span>  
 <span data-ttu-id="39a71-122">[使用者登入](api-management-template-data-model-reference.md#UseSignIn)實體。</span><span class="sxs-lookup"><span data-stu-id="39a71-122">[User sign in](api-management-template-data-model-reference.md#UseSignIn) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="39a71-123">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="39a71-123">Sample template data</span></span>  
  
```json  
{  
    "Email": null,  
    "Password": null,  
    "ReturnUrl": null,  
    "RememberMe": false,  
    "RegistrationEnabled": true,  
    "DelegationEnabled": false,  
    "DelegationUrl": null,  
    "SsoSignUpUrl": null,  
    "AuxServiceUrl": "https://manage.windowsazure.com/#Workspaces/ApiManagementExtension/service/contoso5/dashboard",  
    "Providers": [  
        {  
            "Properties": {  
                "AuthenticationType": "Aad",  
                "Caption": "Azure Active Directory"  
            },  
            "AuthenticationType": "Aad",  
            "Caption": "Azure Active Directory"  
        }  
    ],  
    "UserRegistrationTerms": null,  
    "UserRegistrationTermsEnabled": false  
}  
```  
  
##  <span data-ttu-id="39a71-124"><a name="SignUp"></a> 註冊</span><span class="sxs-lookup"><span data-stu-id="39a71-124"><a name="SignUp"></a> Sign up</span></span>  
 <span data-ttu-id="39a71-125">「註冊」範本可讓您自訂開發人員入口網站中的註冊頁面。</span><span class="sxs-lookup"><span data-stu-id="39a71-125">The **sign up** template allows you to customize the sign up page in the developer portal.</span></span>  
  
 <span data-ttu-id="39a71-126">![註冊頁面](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "APIM 註冊頁面開發人員入口網站範本")</span><span class="sxs-lookup"><span data-stu-id="39a71-126">![Sign Up Page](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "APIM Sign Up Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="39a71-127">預設範本</span><span class="sxs-lookup"><span data-stu-id="39a71-127">Default template</span></span>  
  
```xml  
<h2 class="text-center">{% localized "SignupStrings|PageTitleSignup" %}</h2>  
<p class="text-center">  
  {% localized "SignupStrings|WebAuthenticationAlreadyAMember" %} <a href="/signin">{% localized "SignupStrings|WebAuthenticationSigninNow" %}</a>  
</p>  
  
<div class="row center-block ap-idp-container">  
  <div class="col-md-6">  
    <p>{% localized "SignupStrings|WebAuthenticationCreateNewAccount" %}</p>  
    <sign-up></sign-up>  
  </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="39a71-128">控制</span><span class="sxs-lookup"><span data-stu-id="39a71-128">Controls</span></span>  
 <span data-ttu-id="39a71-129">此範本可能會使用下列[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="39a71-129">This template may  use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="39a71-130">sign-up</span><span class="sxs-lookup"><span data-stu-id="39a71-130">sign-up</span></span>](api-management-page-controls.md#sign-up)  
  
### <a name="data-model"></a><span data-ttu-id="39a71-131">資料模型</span><span class="sxs-lookup"><span data-stu-id="39a71-131">Data model</span></span>  
 <span data-ttu-id="39a71-132">[使用者註冊](api-management-template-data-model-reference.md#UserSignUp)實體。</span><span class="sxs-lookup"><span data-stu-id="39a71-132">[User sign up](api-management-template-data-model-reference.md#UserSignUp) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="39a71-133">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="39a71-133">Sample template data</span></span>  
  
```json  
{  
    "PasswordConfirm": null,  
    "Password": null,  
    "PasswordVerdictLevel": 0,  
    "UserRegistrationTerms": null,  
    "UserRegistrationTermsOptions": 0,  
    "ConsentAccepted": false,  
    "Email": null,  
    "FirstName": null,  
    "LastName": null,  
    "UserData": null,  
    "NameIdentifier": null,  
    "ProviderName": null  
}  
```  
  
##  <span data-ttu-id="39a71-134"><a name="PageNotFound"></a> 找不到頁面</span><span class="sxs-lookup"><span data-stu-id="39a71-134"><a name="PageNotFound"></a> Page not found</span></span>  
 <span data-ttu-id="39a71-135">「找不到頁面」範本可讓您自訂開發人員入口網站中的「找不到頁面」頁面。</span><span class="sxs-lookup"><span data-stu-id="39a71-135">The **page not found** template allows you to customize the page not found page in the developer portal.</span></span>  
  
 <span data-ttu-id="39a71-136">![找不到頁面](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM 找不到頁面開發人員入口網站範本")</span><span class="sxs-lookup"><span data-stu-id="39a71-136">![Not Found Page](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM Not Found Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="39a71-137">預設範本</span><span class="sxs-lookup"><span data-stu-id="39a71-137">Default template</span></span>  
  
```xml  
<h2>{% localized "NotFoundStrings|PageTitleNotFound" %}</h2>  
  
<h3>{% localized "NotFoundStrings|TitlePotentialCause" %}</h3>  
<ul>  
  <li>{% localized "NotFoundStrings|TextblockPotentialCauseOldLink" %}</li>  
  <li>{% localized "NotFoundStrings|TextblockPotentialCauseMisspelledUrl" %}</li>  
</ul>  
  
<h3>{% localized "NotFoundStrings|TitlePotentialSolution" %}</h3>  
<ul>  
  <li>{% localized "NotFoundStrings|TextblockPotentialSolutionRetype" %}</li>  
  <li>  
    {% capture textPotentialSolutionStartOver %}{% localized "NotFoundStrings|TextblockPotentialSolutionStartOver" %}{% endcapture %}  
    {% capture homeLink %}<a href="/">{% localized "NotFoundStrings|LinkLabelHomePage" %}</a>{% endcapture %}  
    {% assign replaceString = '{0}' %}  
  
    {{ textPotentialSolutionStartOver | replace : replaceString, homeLink }}  
  </li>  
</ul>  
  
<p>  
  {% capture textReportProblem %}{% localized "NotFoundStrings|TextReportProblem" %}{% endcapture %}  
  {% capture emailLink %}<a href="mailto:apimgmt@microsoft.com" target="_self" title="API Management Support">{% localized "NotFoundStrings|LinkLabelSendUsEmail" %}</a>{% endcapture %}  
  {% assign replaceString = '{0}' %}  
  
  {{ textReportProblem | replace : replaceString, emailLink }}  
</p>  
```  
  
### <a name="controls"></a><span data-ttu-id="39a71-138">控制</span><span class="sxs-lookup"><span data-stu-id="39a71-138">Controls</span></span>  
 <span data-ttu-id="39a71-139">此範本可能不使用任何[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="39a71-139">This template may  not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="39a71-140">資料模型</span><span class="sxs-lookup"><span data-stu-id="39a71-140">Data model</span></span>  
  
|<span data-ttu-id="39a71-141">屬性</span><span class="sxs-lookup"><span data-stu-id="39a71-141">Property</span></span>|<span data-ttu-id="39a71-142">類型</span><span class="sxs-lookup"><span data-stu-id="39a71-142">Type</span></span>|<span data-ttu-id="39a71-143">說明</span><span class="sxs-lookup"><span data-stu-id="39a71-143">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="39a71-144">referenceCode</span><span class="sxs-lookup"><span data-stu-id="39a71-144">referenceCode</span></span>|<span data-ttu-id="39a71-145">字串</span><span class="sxs-lookup"><span data-stu-id="39a71-145">string</span></span>|<span data-ttu-id="39a71-146">因發生內部錯誤而顯示此頁面時所產生的代碼。</span><span class="sxs-lookup"><span data-stu-id="39a71-146">Code generated if this page was displayed as the result of an internal error.</span></span>|  
|<span data-ttu-id="39a71-147">errorCode</span><span class="sxs-lookup"><span data-stu-id="39a71-147">errorCode</span></span>|<span data-ttu-id="39a71-148">字串</span><span class="sxs-lookup"><span data-stu-id="39a71-148">string</span></span>|<span data-ttu-id="39a71-149">因發生內部錯誤而顯示此頁面時所產生的代碼。</span><span class="sxs-lookup"><span data-stu-id="39a71-149">Code generated if this page was displayed as the result of an internal error.</span></span>|  
|<span data-ttu-id="39a71-150">emailBody</span><span class="sxs-lookup"><span data-stu-id="39a71-150">emailBody</span></span>|<span data-ttu-id="39a71-151">字串</span><span class="sxs-lookup"><span data-stu-id="39a71-151">string</span></span>|<span data-ttu-id="39a71-152">因發生內部錯誤而顯示此頁面時所產生的電子郵件本文。</span><span class="sxs-lookup"><span data-stu-id="39a71-152">Email body generated if this page was displayed as the result of an internal error.</span></span>|  
|<span data-ttu-id="39a71-153">requestedUrl</span><span class="sxs-lookup"><span data-stu-id="39a71-153">requestedUrl</span></span>|<span data-ttu-id="39a71-154">字串</span><span class="sxs-lookup"><span data-stu-id="39a71-154">string</span></span>|<span data-ttu-id="39a71-155">找不到頁面時所要求的 URL。</span><span class="sxs-lookup"><span data-stu-id="39a71-155">The URL requested when the page was not found.</span></span>|  
|<span data-ttu-id="39a71-156">referrerUrl</span><span class="sxs-lookup"><span data-stu-id="39a71-156">referrerUrl</span></span>|<span data-ttu-id="39a71-157">字串</span><span class="sxs-lookup"><span data-stu-id="39a71-157">string</span></span>|<span data-ttu-id="39a71-158">所要求 URL 的查閱者 URL。</span><span class="sxs-lookup"><span data-stu-id="39a71-158">The referrer URL to the requested URL.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="39a71-159">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="39a71-159">Sample template data</span></span>  
  
```json  
{  
    "referenceCode": null,  
    "errorCode": null,  
    "emailBody": null,  
    "requestedUrl": "https://contoso5.portal.azure-api.net:443/NotFoundPage?startEditTemplate=NotFoundPage",  
    "referrerUrl": "https://contoso5.portal.azure-api.net/signup?startEditTemplate=SignUpTemplate"  
}  
```

## <a name="next-steps"></a><span data-ttu-id="39a71-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="39a71-160">Next steps</span></span>
<span data-ttu-id="39a71-161">如需有關使用範本的詳細資訊，請參閱[如何使用範本自訂 API 管理開發人員入口網站](api-management-developer-portal-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="39a71-161">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>