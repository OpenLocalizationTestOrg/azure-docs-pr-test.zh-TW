---
title: "開始在 Visual Studio MVC 專案中使用 Azure AD | Microsoft Docs"
description: "使用 Visual Studio 已連接服務連接 Azure AD 或建立 Azure AD 後，如何在 MVC 專案中開始使用 Azure Active Directory"
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
ms.openlocfilehash: c4d49cfc9887e422b3eaed2b96348c99eca48881
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-azure-active-directory-and-visual-studio-connected-services-mvc-projects"></a><span data-ttu-id="19456-103">開始使用 Azure Active Directory 和 Visual Studio 已連接服務 (MVC 專案)</span><span class="sxs-lookup"><span data-stu-id="19456-103">Getting Started with Azure Active Directory and Visual Studio connected services (MVC Projects)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="19456-104">開始使用</span><span class="sxs-lookup"><span data-stu-id="19456-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="19456-105">發生什麼情形</span><span class="sxs-lookup"><span data-stu-id="19456-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="requiring-authentication-to-access-controllers"></a><span data-ttu-id="19456-106">存取控制器之前需要驗證</span><span class="sxs-lookup"><span data-stu-id="19456-106">Requiring authentication to access controllers</span></span>
<span data-ttu-id="19456-107">專案中的所有控制器都加上 **Authorize** 屬性做裝飾。</span><span class="sxs-lookup"><span data-stu-id="19456-107">All controllers in your project were adorned with the **Authorize** attribute.</span></span> <span data-ttu-id="19456-108">此屬性要求使用者必須經過驗證，才能存取這些控制器。</span><span class="sxs-lookup"><span data-stu-id="19456-108">This attribute requires the user to be authenticated before accessing these controllers.</span></span> <span data-ttu-id="19456-109">若要允許以匿名方式存取控制器，請從控制器中移除此屬性。</span><span class="sxs-lookup"><span data-stu-id="19456-109">To allow the controller to be accessed anonymously, remove this attribute from the controller.</span></span> <span data-ttu-id="19456-110">如果您要以更精確地設定權限，請將此屬性套用至每一個需要授權的方法，而非套用至控制器類別。</span><span class="sxs-lookup"><span data-stu-id="19456-110">If you want to set the permissions at a more granular level, apply the attribute to each method that requires authorization instead of applying it to the controller class.</span></span>

## <a name="adding-signin--signout-controls"></a><span data-ttu-id="19456-111">加入 SignIn / SignOut 控制項</span><span class="sxs-lookup"><span data-stu-id="19456-111">Adding SignIn / SignOut Controls</span></span>
<span data-ttu-id="19456-112">若要將 SignIn/SignOut 控制項新增至檢視，您可以使用 **_LoginPartial.cshtml** 部分檢視，將此功能新增至您的其中一個檢視。</span><span class="sxs-lookup"><span data-stu-id="19456-112">To add the SignIn/SignOut controls to your view, you can use the **_LoginPartial.cshtml** partial view to add the functionality to one of your views.</span></span> <span data-ttu-id="19456-113">以下是新增至標準 **_Layout.cshtml** 檢視的功能範例。</span><span class="sxs-lookup"><span data-stu-id="19456-113">Here is an example of the functionality added to the standard **_Layout.cshtml** view.</span></span> <span data-ttu-id="19456-114">(請注意 div 中具有類別 navbar-collapse 的最後一個元素)：</span><span class="sxs-lookup"><span data-stu-id="19456-114">(Note the last element in the div with class navbar-collapse):</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="19456-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="19456-115">Next steps</span></span>
- [<span data-ttu-id="19456-116">深入了解 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="19456-116">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/) 

