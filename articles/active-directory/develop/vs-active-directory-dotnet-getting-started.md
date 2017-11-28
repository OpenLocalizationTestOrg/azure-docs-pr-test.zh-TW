---
title: "開始使用 Visual Studio MVC 專案中的 Azure AD aaaGet |Microsoft 文件"
description: "Tooget 啟動連接 tooor 建立 Azure AD 使用 Visual Studio 之後，在 MVC 專案中使用 Azure Active Directory 已連接服務"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1c8b6a58-5144-4965-a905-625b9ee7b22b
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 807824dd6e4e57e443f8a7322cf2e5326384316d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-and-visual-studio-connected-services-mvc-projects"></a><span data-ttu-id="3aabc-103">開始使用 Azure Active Directory 和 Visual Studio 已連接服務 (MVC 專案)</span><span class="sxs-lookup"><span data-stu-id="3aabc-103">Getting Started with Azure Active Directory and Visual Studio connected services (MVC Projects)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3aabc-104">開始使用</span><span class="sxs-lookup"><span data-stu-id="3aabc-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="3aabc-105">發生什麼情形</span><span class="sxs-lookup"><span data-stu-id="3aabc-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="requiring-authentication-tooaccess-controllers"></a><span data-ttu-id="3aabc-106">需要驗證 tooaccess 控制站</span><span class="sxs-lookup"><span data-stu-id="3aabc-106">Requiring authentication tooaccess controllers</span></span>
<span data-ttu-id="3aabc-107">在您的專案中的所有控制站已裝飾以 hello**授權**屬性。</span><span class="sxs-lookup"><span data-stu-id="3aabc-107">All controllers in your project were adorned with hello **Authorize** attribute.</span></span> <span data-ttu-id="3aabc-108">此屬性需要驗證才能存取這些控制站的 hello 使用者 toobe。</span><span class="sxs-lookup"><span data-stu-id="3aabc-108">This attribute requires hello user toobe authenticated before accessing these controllers.</span></span> <span data-ttu-id="3aabc-109">以匿名方式，存取 tooallow hello 控制器 toobe 從 hello 控制器移除這個屬性。</span><span class="sxs-lookup"><span data-stu-id="3aabc-109">tooallow hello controller toobe accessed anonymously, remove this attribute from hello controller.</span></span> <span data-ttu-id="3aabc-110">如果您想 tooset hello 權限，在更細微的層級，套用 hello 屬性 tooeach 方法，會要求授權，而不是套用它 toohello 控制器類別。</span><span class="sxs-lookup"><span data-stu-id="3aabc-110">If you want tooset hello permissions at a more granular level, apply hello attribute tooeach method that requires authorization instead of applying it toohello controller class.</span></span>

## <a name="adding-signin--signout-controls"></a><span data-ttu-id="3aabc-111">加入 SignIn / SignOut 控制項</span><span class="sxs-lookup"><span data-stu-id="3aabc-111">Adding SignIn / SignOut Controls</span></span>
<span data-ttu-id="3aabc-112">tooadd hello 登入/登出控制 tooyour 檢視，您可以使用 hello **_LoginPartial.cshtml**部分檢視 tooadd hello 功能 tooone 的檢視。</span><span class="sxs-lookup"><span data-stu-id="3aabc-112">tooadd hello SignIn/SignOut controls tooyour view, you can use hello **_LoginPartial.cshtml** partial view tooadd hello functionality tooone of your views.</span></span> <span data-ttu-id="3aabc-113">以下是範例的 hello 功能加入的 toohello 標準**_Layout.cshtml**檢視。</span><span class="sxs-lookup"><span data-stu-id="3aabc-113">Here is an example of hello functionality added toohello standard **_Layout.cshtml** view.</span></span> <span data-ttu-id="3aabc-114">（請注意 hello hello div 類別導覽列摺疊中的最後一個項目）：</span><span class="sxs-lookup"><span data-stu-id="3aabc-114">(Note hello last element in hello div with class navbar-collapse):</span></span>

<pre>
    &lt;!DOCTYPE html&gt; 
     &lt;html&gt; 
     &lt;head&gt; 
         &lt;meta charset="utf-8" /&gt; 
        &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt; 
        &lt;title&gt;@ViewBag.Title - My ASP.NET Application&lt;/title&gt; 
        @Styles.Render("~/Content/css") 
        @Scripts.Render("~/bundles/modernizr") 
    &lt;/head&gt; 
    &lt;body&gt; 
        &lt;div class="navbar navbar-inverse navbar-fixed-top"&gt; 
            &lt;div class="container"&gt; 
                &lt;div class="navbar-header"&gt; 
                    &lt;button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse"&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                    &lt;/button&gt; 
                    @Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" }) 
                &lt;/div&gt; 
                &lt;div class="navbar-collapse collapse"&gt; 
                    &lt;ul class="nav navbar-nav"&gt; 
                        &lt;li&gt;@Html.ActionLink("Home", "Index", "Home")&lt;/li&gt; 
                        &lt;li&gt;@Html.ActionLink("About", "About", "Home")&lt;/li&gt; 
                        &lt;li&gt;@Html.ActionLink("Contact", "Contact", "Home")&lt;/li&gt; 
                    &lt;/ul&gt; 
                    <span style="background-color:yellow">@Html.Partial("_LoginPartial")</span> 
                &lt;/div&gt; 
            &lt;/div&gt; 
        &lt;/div&gt; 
        &lt;div class="container body-content"&gt; 
            @RenderBody() 
            &lt;hr /&gt; 
            &lt;footer&gt; 
                &lt;p&gt;&amp;copy; @DateTime.Now.Year - My ASP.NET Application&lt;/p&gt; 
            &lt;/footer&gt; 
        &lt;/div&gt; 
        @Scripts.Render("~/bundles/jquery") 
        @Scripts.Render("~/bundles/bootstrap") 
        @RenderSection("scripts", required: false) 
    &lt;/body&gt; 
    &lt;/html&gt;
</pre>

## <a name="next-steps"></a><span data-ttu-id="3aabc-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3aabc-115">Next steps</span></span>
- [<span data-ttu-id="3aabc-116">深入了解 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3aabc-116">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/) 

