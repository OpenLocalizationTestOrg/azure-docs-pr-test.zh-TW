---
title: "在 Azure API 管理 aaaPage 範本 |Microsoft 文件"
description: "了解如何 toocustomize hello 使用一組範本，在 Azure API 管理開發人員入口網站頁面的內容。"
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
ms.openlocfilehash: 84bd971ad4bcacfdd36c2ebbe05b16063f2a547b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="page-templates-in-azure-api-management"></a><span data-ttu-id="8208b-103">Azure API 管理中的頁面範本</span><span class="sxs-lookup"><span data-stu-id="8208b-103">Page templates in Azure API Management</span></span>
<span data-ttu-id="8208b-104">Azure API 管理提供 hello 能力 toocustomize hello 網頁內容的開發人員入口網站使用的一組設定其內容的範本。</span><span class="sxs-lookup"><span data-stu-id="8208b-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="8208b-105">使用[DotLiquid](http://dotliquidmarkup.org/)語法和 hello 您選擇的編輯器例如[針對設計人員 DotLiquid](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers)，和一組提供的當地語系化[字串資源](api-management-template-resources.md#strings)， [字符資源](api-management-template-resources.md#glyphs)，和[頁面控制項](api-management-page-controls.md)，視使用這些範本，您會有很大的彈性 tooconfigure hello 網頁內容的 hello。</span><span class="sxs-lookup"><span data-stu-id="8208b-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="8208b-106">本節中的 hello 範本可讓您 toocustomize hello 內容 hello 登入，登，以及頁面中找不到頁面 hello 開發人員入口網站。</span><span class="sxs-lookup"><span data-stu-id="8208b-106">hello templates in this section allow you toocustomize hello content of hello sign in, sign up, and page not found pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="8208b-107">登入</span><span class="sxs-lookup"><span data-stu-id="8208b-107">Sign in</span></span>](#SignIn)  
  
-   [<span data-ttu-id="8208b-108">註冊</span><span class="sxs-lookup"><span data-stu-id="8208b-108">Sign up</span></span>](#SignUp)  
  
-   [<span data-ttu-id="8208b-109">找不到頁面</span><span class="sxs-lookup"><span data-stu-id="8208b-109">Page not found</span></span>](#PageNotFound)  
  
> [!NOTE]
>  <span data-ttu-id="8208b-110">預設範本範例隨附的 hello 下列文件，但主旨 toochange 到期 toocontinuous 增強功能。</span><span class="sxs-lookup"><span data-stu-id="8208b-110">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="8208b-111">您可以檢視 hello 開發人員入口網站中的 hello 即時預設範本，藉由瀏覽 toohello 需要個別的範本。</span><span class="sxs-lookup"><span data-stu-id="8208b-111">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="8208b-112">如需有關使用範本的詳細資訊，請參閱[toocustomize hello API 管理開發人員入口網站使用範本的方式](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)。</span><span class="sxs-lookup"><span data-stu-id="8208b-112">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="8208b-113"><a name="SignIn"></a> 登入</span><span class="sxs-lookup"><span data-stu-id="8208b-113"><a name="SignIn"></a> Sign in</span></span>  
 <span data-ttu-id="8208b-114">hello**登入**範本可讓您 toocustomize hello 登在 hello 開發人員入口網站 頁面中。</span><span class="sxs-lookup"><span data-stu-id="8208b-114">hello **sign in** template allows you toocustomize hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="8208b-115">![登入頁面](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM 登入頁面開發人員入口網站範本")</span><span class="sxs-lookup"><span data-stu-id="8208b-115">![Sign In Page](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM Sign In Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="8208b-116">預設範本</span><span class="sxs-lookup"><span data-stu-id="8208b-116">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="8208b-117">控制</span><span class="sxs-lookup"><span data-stu-id="8208b-117">Controls</span></span>  
 <span data-ttu-id="8208b-118">此範本可能會使用 hello 下列[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="8208b-118">This template may  use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="8208b-119">basic-signin</span><span class="sxs-lookup"><span data-stu-id="8208b-119">basic-signin</span></span>](api-management-page-controls.md#basic-signin)  
  
-   [<span data-ttu-id="8208b-120">提供者</span><span class="sxs-lookup"><span data-stu-id="8208b-120">providers</span></span>](api-management-page-controls.md#providers)  
  
### <a name="data-model"></a><span data-ttu-id="8208b-121">資料模型</span><span class="sxs-lookup"><span data-stu-id="8208b-121">Data model</span></span>  
 <span data-ttu-id="8208b-122">[使用者登入](api-management-template-data-model-reference.md#UseSignIn)實體。</span><span class="sxs-lookup"><span data-stu-id="8208b-122">[User sign in](api-management-template-data-model-reference.md#UseSignIn) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="8208b-123">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="8208b-123">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="8208b-124"><a name="SignUp"></a> 註冊</span><span class="sxs-lookup"><span data-stu-id="8208b-124"><a name="SignUp"></a> Sign up</span></span>  
 <span data-ttu-id="8208b-125">hello**註冊**範本可讓您 toocustomize hello 登入頁面 hello 開發人員入口網站中。</span><span class="sxs-lookup"><span data-stu-id="8208b-125">hello **sign up** template allows you toocustomize hello sign up page in hello developer portal.</span></span>  
  
 <span data-ttu-id="8208b-126">![註冊頁面](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "APIM 註冊頁面開發人員入口網站範本")</span><span class="sxs-lookup"><span data-stu-id="8208b-126">![Sign Up Page](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "APIM Sign Up Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="8208b-127">預設範本</span><span class="sxs-lookup"><span data-stu-id="8208b-127">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="8208b-128">控制</span><span class="sxs-lookup"><span data-stu-id="8208b-128">Controls</span></span>  
 <span data-ttu-id="8208b-129">此範本可能會使用 hello 下列[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="8208b-129">This template may  use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="8208b-130">sign-up</span><span class="sxs-lookup"><span data-stu-id="8208b-130">sign-up</span></span>](api-management-page-controls.md#sign-up)  
  
### <a name="data-model"></a><span data-ttu-id="8208b-131">資料模型</span><span class="sxs-lookup"><span data-stu-id="8208b-131">Data model</span></span>  
 <span data-ttu-id="8208b-132">[使用者註冊](api-management-template-data-model-reference.md#UserSignUp)實體。</span><span class="sxs-lookup"><span data-stu-id="8208b-132">[User sign up](api-management-template-data-model-reference.md#UserSignUp) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="8208b-133">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="8208b-133">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="8208b-134"><a name="PageNotFound"></a> 找不到頁面</span><span class="sxs-lookup"><span data-stu-id="8208b-134"><a name="PageNotFound"></a> Page not found</span></span>  
 <span data-ttu-id="8208b-135">hello**找不到頁面**範本可讓您 toocustomize hello 找不到頁面頁面 hello 開發人員入口網站中。</span><span class="sxs-lookup"><span data-stu-id="8208b-135">hello **page not found** template allows you toocustomize hello page not found page in hello developer portal.</span></span>  
  
 <span data-ttu-id="8208b-136">![找不到頁面](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM 找不到頁面開發人員入口網站範本")</span><span class="sxs-lookup"><span data-stu-id="8208b-136">![Not Found Page](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM Not Found Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="8208b-137">預設範本</span><span class="sxs-lookup"><span data-stu-id="8208b-137">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="8208b-138">控制</span><span class="sxs-lookup"><span data-stu-id="8208b-138">Controls</span></span>  
 <span data-ttu-id="8208b-139">此範本可能不使用任何[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="8208b-139">This template may  not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="8208b-140">資料模型</span><span class="sxs-lookup"><span data-stu-id="8208b-140">Data model</span></span>  
  
|<span data-ttu-id="8208b-141">屬性</span><span class="sxs-lookup"><span data-stu-id="8208b-141">Property</span></span>|<span data-ttu-id="8208b-142">類型</span><span class="sxs-lookup"><span data-stu-id="8208b-142">Type</span></span>|<span data-ttu-id="8208b-143">說明</span><span class="sxs-lookup"><span data-stu-id="8208b-143">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="8208b-144">referenceCode</span><span class="sxs-lookup"><span data-stu-id="8208b-144">referenceCode</span></span>|<span data-ttu-id="8208b-145">字串</span><span class="sxs-lookup"><span data-stu-id="8208b-145">string</span></span>|<span data-ttu-id="8208b-146">如果此頁面顯示 hello 發生內部錯誤導致產生的程式碼。</span><span class="sxs-lookup"><span data-stu-id="8208b-146">Code generated if this page was displayed as hello result of an internal error.</span></span>|  
|<span data-ttu-id="8208b-147">errorCode</span><span class="sxs-lookup"><span data-stu-id="8208b-147">errorCode</span></span>|<span data-ttu-id="8208b-148">字串</span><span class="sxs-lookup"><span data-stu-id="8208b-148">string</span></span>|<span data-ttu-id="8208b-149">如果此頁面顯示 hello 發生內部錯誤導致產生的程式碼。</span><span class="sxs-lookup"><span data-stu-id="8208b-149">Code generated if this page was displayed as hello result of an internal error.</span></span>|  
|<span data-ttu-id="8208b-150">emailBody</span><span class="sxs-lookup"><span data-stu-id="8208b-150">emailBody</span></span>|<span data-ttu-id="8208b-151">字串</span><span class="sxs-lookup"><span data-stu-id="8208b-151">string</span></span>|<span data-ttu-id="8208b-152">如果此頁面顯示 hello 發生內部錯誤導致產生的內文的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="8208b-152">Email body generated if this page was displayed as hello result of an internal error.</span></span>|  
|<span data-ttu-id="8208b-153">requestedUrl</span><span class="sxs-lookup"><span data-stu-id="8208b-153">requestedUrl</span></span>|<span data-ttu-id="8208b-154">字串</span><span class="sxs-lookup"><span data-stu-id="8208b-154">string</span></span>|<span data-ttu-id="8208b-155">hello 時找不到 hello 頁面要求的 URL。</span><span class="sxs-lookup"><span data-stu-id="8208b-155">hello URL requested when hello page was not found.</span></span>|  
|<span data-ttu-id="8208b-156">referrerUrl</span><span class="sxs-lookup"><span data-stu-id="8208b-156">referrerUrl</span></span>|<span data-ttu-id="8208b-157">字串</span><span class="sxs-lookup"><span data-stu-id="8208b-157">string</span></span>|<span data-ttu-id="8208b-158">hello 查閱者 URL toohello 要求的 URL。</span><span class="sxs-lookup"><span data-stu-id="8208b-158">hello referrer URL toohello requested URL.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="8208b-159">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="8208b-159">Sample template data</span></span>  
  
```json  
{  
    "referenceCode": null,  
    "errorCode": null,  
    "emailBody": null,  
    "requestedUrl": "https://contoso5.portal.azure-api.net:443/NotFoundPage?startEditTemplate=NotFoundPage",  
    "referrerUrl": "https://contoso5.portal.azure-api.net/signup?startEditTemplate=SignUpTemplate"  
}  
```

## <a name="next-steps"></a><span data-ttu-id="8208b-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8208b-160">Next steps</span></span>
<span data-ttu-id="8208b-161">如需有關使用範本的詳細資訊，請參閱[toocustomize hello API 管理開發人員入口網站使用範本的方式](api-management-developer-portal-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="8208b-161">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
